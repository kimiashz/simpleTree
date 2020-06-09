<template>
  <div class="tree">
    <tree-component :tree="tree"/>
  </div>
</template>

<script>
import TreeComponent from '../components/Tree.vue';

export default {
  name: 'tree',
  data: function(){
    let make = this.makeNode;
    return {
      tree:make('www',[
            make('etc',[
              make('apache'),
              make('nginx',[make('file.config')]),
              make('consul',[make('config.json'),make('data')])
            ]),
            make('hosts'),
            make('readme')
          ])
    }
  },
  components:{
    TreeComponent
  },
  methods:{
    makeNode:function(name,children){
      var node = {name};
      if(Array.isArray(children)) node.children = children;
      return node;
    }
  }
}
</script>