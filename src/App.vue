<template>
  <div id="app">
    <LineChart :data="dataset"/>
  </div>
</template>

<script>
import LineChart from "./components/LineChart";

export default {
  name: "App",
  components: {
    LineChart
  },
  data() {
    return {
      dataset: [
        { y: 115 },
        { y: 117 },
        { y: 119 },
        { y: 109 },
        { y: 113 },
        { y: 110 },
        { y: 115 }
      ]
    };
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
