<template>
  <div class="hello">
    <h1>{{title}}</h1>
    <p>{{message}}</p>
    <hr>
    <div>Value: <input type="number" v-model="val"></div>
    <div>Value2: <input type="number" v-model="val2"></div>

    <div style="height:10px;"></div>
    <table>
      <tr>
        <th>add:</th>
        <td>{{add}}</td>
      </tr>
      <tr>
        <th>sub:</th>
        <td>{{sub}}</td>
      </tr>
      <tr>
        <th>mult:</th>
        <td>{{mult}}</td>
      </tr>
      <tr>
        <th>divide:</th>
        <td>{{div}}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  // 自分の名前(個要素だから)
  name: 'Enzan',
  props: {
    title: String,
  },
  data: function(){
    return{
      message: '値の監視',
      val: 0,
      val2: 0
    };
  },
  computed: {
    // 足算 画面の val1 と val2の値を足し合わせている
    add: function(){
      return Math.floor(this.val) + Math.floor(this.val2)
    },
    sub: function(){
      return Math.floor(this.val) - Math.floor(this.val2)
    },
    mult: function(){
      return Math.floor(this.val) * Math.floor(this.val2)
    },
    div: function(){
      return Math.floor(this.val) / Math.floor(this.val2)
    }
  },
  created: function(){
    this.val = 5;
    this.val2 = 5;
  },
}
</script>