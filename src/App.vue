<template>
  <div id="app">
   <navigation/>
    <router-view/>
  </div>
</template>

<script>
import Navigation from './components/Navigation.vue';
export default {
  name: 'app',
  components:{
    Navigation
  }
}
</script>

<style lang="sass">
@import './sass/main.sass'

#nav 
  padding: $padding
  width: 100%
  a 
    font-weight: bold
    color: $gray
    display: inline-block

    &.router-link-exact-active 
      color: $color
    
</style>
