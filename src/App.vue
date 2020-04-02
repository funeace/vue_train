<template>
  <div id="app">
    <!-- 親要素から子要素へ、バインドを行っている。さらに、イベントが発生したらappActionが発火するようにしている -->
    <Calc v-bind:title="message" v-on:result-event="appAction" />
    <hr>
    <div>
      <table v-html="log"></table>
    </div>
  </div>
</template>

<script>
import Calc from './components/Calc.vue'

export default {
 name: 'app',
 components: {
   Calc
  } ,
  data: function(){
    return {
      message: 'CALC',
      result: [],
    };
  },
  computed: {
    // 算出プロパティとして定義
    log:function(){
      var table = '<tr><th class="head>Expression</th><th class="head">Value</th></tr>';
      for(var i in this.result){
        table += '<tr><td>' + this.result[i][0] + '</td><th>' + this.result[i][1] + '</th></tr>';
      }
      return table;
    }
  },
  // 初期化を行う処理
  created: function(){
    // webブラウザ上でクライアントのデータを保存する仕組み
    var items = localStorage.getItem('log');
    // itemsで保存したデータをJSON形式に変換している。
    var logs = JSON.parse(items);
    if (logs != null){ this.result = logs;}
  },
  // ロードされたタイミングで呼び出される
  methods:{
    // v-onしたときにバインド（同期）されるプロパティ。引数二つ？
    appAction: function(exp,res) {
    // 引数を配列resultに追加
    this.result.unshift([exp,res]);
    // resultの項目数が10を超えていたら一番後ろを削除(pop)
    if (this.result.length > 10){
      this.result.pop();
    }
    // 引数のオブジェクトをJSON形式のテキストに変換している
    var log = JSON.stringify(this.result);
    // 更新した値がログとして表示される
    localStorage.setItem('log',log);
    }
  }
}
</script>

