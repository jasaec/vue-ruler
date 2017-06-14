<template>
  <div id="app">
    <input v-model="length" placeholder="input ruler length">
    <div style="margin-left: 20px;margin-top:30px">
      <ruler :range="length" style="margin-left:10px" :numeralsStyle="numeralsStyle"></ruler>
      <ruler :range="length" mode="vertical" markColor="#1DBCE0"></ruler>
    </div>
  </div>
</template>
<script>
import ruler from './ruler.vue'

export default {
  name: 'app',
  components: {
    ruler
  },
  data () {
    return {
      length: 10,
      numeralsStyle: {color: 'red', 'font-size': '15px'}
    }
  }
}
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
