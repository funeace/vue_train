<template>
  <div class="hello">
    <h1>{{title}}</h1>
    <p>{{message}}</p>
    <hr>
    <p>Number: {{ num }}</p>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    title: String,
    num: Number,
  },

  data:function(){
    return {
      message: 'バリデーションチェック',
    };
  },
}
</script>