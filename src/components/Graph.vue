<template>
  <div class='chartAreaContainer'>
    <h4>
      Adjust the Equilibrium Yourself!
    </h4>
    <div class="chartWrapper">
      <div class="supplyLine"></div>
      <div class="demandLine"></div>
      <span class='yAxisTitle'>Price</span>
      <span class='xAxisTitle'>Quantity</span>
    </div>
    <div class="btnContainer">
      <button 
        type='button' 
        v-for='(btn, idx) in btnArr' 
        :key='idx'
      >
        {{ btn.value }}
      </button>
    </div>
  </div>


</template>


<script>
  export default {
    
    name: 'graph',


    data() {
      return {
        btnArr: [
          {
            value: 'Reduce Supply',
            selected: false,
          },
          {
            value: 'Increase Supply',
            selected: false,
          },
        ]
      }
    },
  }
</script>



<style scoped>
  h4 {
    color: var(--clr-darkBg);
    margin-bottom: 1em;
    text-align: center;
  }

  .chartAreaContainer {
    padding: 1.5rem;
  }

  .chartWrapper {
    height: 15rem;
    border-left: 1px solid black;
    border-bottom: 1px solid black;
    position: relative;
  }

  .supplyLine {
    position: absolute;
    width: 275px; 
    height: 100px;  
    border: solid 2px #000;
    border-color: var(--clr-accent) transparent transparent transparent;
    border-radius: 50%/20px 60px 0 0;
    transform: rotate(140deg);
    bottom: 25%;
  }

  .demandLine {
    position: absolute;
    width: 275px; 
    height: 100px;  
    border: solid 2px #000;
    border-color: var(--clr-darkBg) transparent transparent transparent;
    border-radius: 50%/20px 60px 0 0;
    transform: rotate(220deg);
    bottom: 30%;
    left: 20%;
  }

  .yAxisTitle {
    color: var(--clr-accent);
    position: absolute;
    left: -1.9rem;
    bottom: 50%;
    transform: rotate(-90deg);
    font-weight: 600;
  }

  .xAxisTitle {
    color: var(--clr-accent);
    position: absolute;
    bottom: -1.5rem;
    left: 50%;
    transform: translateX(-50%);
    font-weight: 600;
  }
</style>
