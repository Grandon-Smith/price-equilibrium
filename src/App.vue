<template>
  <div id="app">
    <Header/>
    <Graph />
  </div>
</template>

<script>
import Graph from './components/Graph.vue'
import Header from './components/Header.vue'

export default {
  name: 'App',





  data() {
    return {

    }
  },




  
  components: {
    Graph,
    Header,
  },





  mounted: function() {

  },
}
</script>

<style>
  :root {
    --clr-darkBg: #555;
    --clr-accent: rgb(75, 138, 233);
  }

  *,
  *::before,
  *::after {
    box-sizing: border-box;
    padding: 0;
    margin: 0;
  }

</style>
