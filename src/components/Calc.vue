<template>
  <div class="hello">
    <h1>{{ title }}</h1>
    <p>{{ message }}</p>
    <hr>
    <div>
      <div><textarea v-model="fomula" 
        cols="40" rows="5"></textarea></div>
      <div><button v-on:click="doAction">CALC</button></div>
    </div>
  </div>
</template>



<script>
// 親要素から出力するための入口を作成
export default {
  name: 'Calc',
  props: {
    title: String,
  },
  data:function(){
    return {
      message: 'Enter expression:',
      fomula:'0',
    };
  },
  // methodsは描画されると関数を実行する
  methods:{
    // doActionがバインドされたときに動く
    doAction: function(){
      // v-modelで呼び出されたfomulaの値をarrに格納
      var arr = this.fomula.trim().split('\n');
      // arrの中身を配列に追加
      var last = arr.pop();
      var fn = '';
      // arr分roopを回す
      for(var n in arr){
        // 配列に値があるとき
        if (arr[n].trim() != ''){
          fn += 'var ' + arr[n] + ';';
        }
      }
      fn += 'return ' + last + ';';
      var exp = 'function f(){' + fn + '} f();';
      // スクリプトを実行する
      var ans = eval(exp);
      this.message = 'answer: ' + ans;
      var re = arr.join(';').trim();
      if (re != '') { re += ';'}
      re += last;
      // 親要素のresult-eventに re と ans を返却
      this.$emit('result-event', re, ans);
    }
  }
}
</script>
