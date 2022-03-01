<template>
  <div id="app">
    <Header/>
    <div class="body">
      <TextExpander
        headerText='Header Text here'
        bodyText='
          Lorem ipsum dolor sit amet consectetur adipisicing elit.
          Consequuntur tempore debitis minus deserunt! Molestias dolorem alias
          voluptatibus reiciendis vitae assumenda sunt amet ad veritatis vero
          nobis autem, distinctio at neque! Architecto facere nuo, est magnam
          ab quia cumque consequatur eos laborum!'
      />
      <Graph />

    </div>

  </div>
</template>

<script>
import Graph from './components/Graph.vue';
import Header from './components/Header.vue';
import TextExpander from './components/TextExpander.vue';

export default {
  name: 'App',





  data() {
    return {

    }
  },




  
  components: {
    Graph,
    Header,
    TextExpander,
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

  #app {
    position: relative;
  }

  .body {
    padding: .5rem .75rem;
  }

</style>
