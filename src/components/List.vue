<template>
    <li>
        <div
            :class="{bold: isFolder}"
            @dblclick="makeFolder"
        >
            {{tree.name}}
            <span @click="toggle" v-if="isFolder">[{{ isOpen ? '-' : '+' }}]</span>
            <span @click="deleteItem">[x]</span>
        </div>
        <ul v-if="isFolder" v-show="isOpen">
            <list 
                v-for="(child, index) in tree.children"
                :key="index"
                :tree="child"
                @make-folder="$emit('make-folder', $event)"
                @add-item="$emit('add-item', $event)"
                @delete-item="$emit('delete-item', $event)"
            ></list>
            <li><input v-model="newItemName"><button @click="addItem">+</button></li>
        </ul>
    </li>
</template>

<script>
export default {
    name:'list',
    props:{
        tree: Object
    },
    data:function(){
        return {
            isOpen: true,
            newItemName: 'new'
        }
    },
    computed:{
        isFolder: function(){
            return Array.isArray(this.tree.children);
        }
    },
    methods:{
        makeFolder:function() {
            if(!this.isFolder){
                this.$emit('make-folder', this.tree);
                this.isOpen = true;
            }
        },
        deleteItem:function() {this.$emit('delete-item', this.tree);},
        addItem:function() { this.$emit('add-item', [this.tree,this.newItemName]); this.newItemName='new';},
        toggle:function() { this.isOpen = !this.isOpen}
    }
}
</script>

<style lang="sass" scoped>
    @import '@/sass/main.sass';

    .list
        ul 
            margin: $margin
            border-left: $border
            li
                margin: $margin

        .message
            padding: $padding
            color: $gray
</style>