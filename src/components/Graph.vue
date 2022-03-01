<template>
  <section class="graphAreaContainer">
    Graph Area
    <canvas id='lineChart' height='100%' width='100%'></canvas>
  </section>
</template>

<script>
export default {
  name: 'Graph',
  

  data() {
    return {
      
    }
  },


  props: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.graphAreaContainer {
  border: 1px solid black;
}

</style>
