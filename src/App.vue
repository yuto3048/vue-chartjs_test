<template>
  <div id="app">
    <img src="./assets/logo.png">
    <ChartTest :data="data" :labels="labels" />
  </div>
</template>

<script>
import ChartTest from './components/ChartTest'
import jsonp from 'jsonp'

export default {
  name: 'App',
  components: {
    ChartTest
  },
  data() {
    return {
      intervalId: undefined,
      labels: [],
      data: []
    }
  },
  methods: {
    getData: function(){
      jsonp('https://api.openweathermap.org/data/2.5/weather?id=1858311&appid=434d547f0abc51b1c0a3f9fc01ee749a', null, (error, data) => {
        if (error) { console.log(error) }
        else {
          var temp = data.main.temp
          var timestamp = data.dt
          console.log(timestamp)
          this.data.push(temp)
          this.labels.push(timestamp)
        }
      })
    }
  },
  created() {
    this.getData
  },
  mounted() {
    var self = this
    this.intervalId = setInterval(function(){self.getData()}, 30000)
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
