<template>
  <div 
    class='chartAreaContainer' 
    aria-label='interactive graph moving supply and demand lines.' 
    tabindex="0"
  >
    <h4 tabindex="0">
      Adjust the Equilibrium Yourself!
    </h4>
    <div class="chartWrapper">
      <div 
        class='lineWrapper' 
        :class='{ reduce : btnArr[0].selected,  increase : btnArr[2].selected}'
      >
        <div class="supplyLine" ></div>
      </div>
      <div class="demandLine"></div>
      <span class='yAxisTitle'>Price</span>
      <span class='xAxisTitle'>Quantity</span>
    </div>
    <div class="btnContainer"
    :class='{ expanded : infoMessage.length }'
    >
      <button 
        :class='btn.classes'
        type='button' 
        v-for='(btn, idx) in btnArr' 
        :key='idx'
        @click='handleBtnClick(idx)'
      >
        {{ btn.value }}
      </button>
    </div>
    <transition name='fadeIn'>
      <p v-if='infoMessage.length' class='errorMsg'>{{ infoMessage }}</p>
    </transition>
  </div>
</template>





<script>
  export default {
    


    name: 'graph',



    data() {
      return {
        infoMessage: '',
        btnArr: [
          {
            value: 'Reduce Supply',
            selected: false,
            classes: 'eqAdjustBtn',
            infoMessage: 'As supply reduces, the price at equilibrium increases'
          },
          {
            value: 'Clear',
            selected: false,
            classes: 'eqAdjustBtn clear'
          },
          {
            value: 'Increase Supply',
            selected: false,
            classes: 'eqAdjustBtn',
            infoMessage: 'As supply increases, the price at equilibrium decreases'
          },
        ]
      }
    },



    methods: {
      handleBtnClick: function(idx=null) {
        for(let i = 0; i < this.btnArr.length; i++) {
          this.btnArr[i].selected = false;
        }

        this.btnArr[idx].selected = true;
        this.infoMessage = this.btnArr[idx].infoMessage ? this.btnArr[idx].infoMessage : ''
      }
    }
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
    max-width: 30rem;
    margin: 0 auto;
    position: relative;
  }

  .chartWrapper {
    height: 15rem;
    border-left: 1px solid black;
    border-bottom: 1px solid black;
    position: relative;
  }

  .lineWrapper {
    position: absolute;
    bottom: 25%;
    transition: transform .3s ease;
  }

  .supplyLine {
    width: 275px; 
    height: 100px;  
    border: solid 2px #000;
    border-color: var(--clr-accent) transparent transparent transparent;
    border-radius: 50%/20px 60px 0 0;
    transform: rotate(140deg);
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

  .reduce {
    transform: translateX(-45px);
  }
  
  .increase {
    transform: translateX(45px);
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

  .btnContainer {
    padding-top: 3rem;
    display: flex;
    justify-content: space-between;
    transition: all .2s ease;
  }
  .btnContainer.expanded {
    padding-bottom: 3rem;
  } 

  .eqAdjustBtn {
    background-color: #fff;
    border: 2px solid var(--clr-accent);
    color: var(--clr-accent);
    font-size: .9rem;
    padding: .25em;
    cursor: pointer;
    transition: all .2s ease;
  }

  .eqAdjustBtn:hover,
  .eqAdjustBtn:focus {
    background-color: var(--clr-accent);
    border: 2px solid var(--clr-accent);
    color: #fff;
    padding: .25em;
    cursor: pointer;
  }

  .clear {
    border: 2px solid rgb(255, 52, 52);
    color: rgb(255, 52, 52);
  }

  .clear:hover,
  .clear:focus {
    border: 2px solid rgb(255, 52, 52);
    background-color: rgb(255, 52, 52);
    color: #fff;
  }

  .errorMsg {
    position: absolute;
    bottom: 1rem;
  }

  .fadeIn-enter-active,
  .fadeIn-leave-active {
    opacity: 1;
  }

  .fadeIn-enter-from,
  .fadeIn-leave-to {
  opacity: 0;
}
</style>
