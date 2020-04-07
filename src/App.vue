<template>
  <div id="app">
    <HelloWorld title="validate" />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  components: {
    HelloWorld
  }  ,
  data: function(){
    return {
      message:'validate',
      num: 'abc',
    };
  }
}
</script>