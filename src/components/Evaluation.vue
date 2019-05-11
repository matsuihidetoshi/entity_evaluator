<template>
  <div class="evaluation">
    <div>名前: <input style="font-size:18px;margin-bottom:10px;" v-model="name"></div>
    <select v-model="positivity">
      <option disabled value="">Please select one</option>
      <option>1</option>
      <option>2</option>
      <option>3</option>
    </select>
    <button v-on:click="evaluate()">投票！</button>
    <div>結果: {{ result }}</div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  name: 'Evaluation',
  props: {
    name: String,
    positivity: Number,
  },
  data(){
    return{
      result: null
    }
  },
  methods: {
    evaluate: function(){
      var headers = {
        'Content-Type': 'application/json',
        'Access-Control-Allow-Origin': '*'
      }
      axios({
        method: 'get',
        url: 'https://5y46it5qkh.execute-api.ap-northeast-1.amazonaws.com/default/EntityEvaluator',
        params: {
          name: this.name,
          positivity: this.positivity
        },
        credentials: true,
        headers: headers
      }).then(response => {
        this.result = response
      })
    }
  }
}
</script>
<style scoped>
</style>