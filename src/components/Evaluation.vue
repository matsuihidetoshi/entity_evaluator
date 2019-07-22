<template>
  <div class="evaluation">
    <div>質問検索: <input style="font-size:18px;margin-bottom:10px;" v-model="name"></div>
    <select v-model="positivity">
      <option disabled value="">Please select one</option>
      <option>1</option>
      <option>2</option>
      <option>3</option>
    </select>
    <button v-on:click="evaluate()">一覧表示</button>
    <div>
      <ol>
        <li v-for="(result, id) in results" v-bind:key="id">
          {{ result.title }}
        </li>
      </ol>
    </div>
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
      results: null
    }
  },
  methods: {
    evaluate: function(){
      axios
      .get('https://quesgen.work/api/questions/?format=json')
      .then(response => (this.results = response.data))
    }
  }
}
</script>
<style scoped>
ul {
  list-style: none;
}
</style>