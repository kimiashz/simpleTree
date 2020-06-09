<template>
    <page title="this is the tree">
        <template v-slot:aside>hi aside</template>
        <ul class="list">
            <list :tree="tree" 
            @make-folder="makeFolder"
            @add-item="addItem"
            @delete-item="deleteItem"
            />
        </ul>
    </page>
</template>

<script>
import Page from './Page.vue';
import List from './List.vue';
export default {
    name: 'treeComponent',
    props:{
        tree: Object
    },
    components: {
        Page,
        List
    },
    methods:{
        makeFolder: function(tree){
            this.$set(tree, 'children', []);
            //this.addItem(tree);
        },
        addItem: function([tree,name]){
            tree.children.push({name});
        },
        deleteItem: function(node){
            let s = this.search(this.tree, node);
            if(s && s.length)
                s[0].splice(s[1],1);
        },
        search:function search(tree, node){
            let {children} = tree;
            if(children && children.length){
                let x = children.indexOf(node);
                if(~x)
                    return [children, x];
                else
                    for(let n of children){ let r =search(n,node); if(r) return r;}
            } else 
                return false;
        }
    }
}
</script>