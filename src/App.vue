<template>
  <div id="app">
    <Header/>
    <p v-if='loadingMsg' class='loadingMsg'>
      {{ loadingMsg }}
    </p>
    <div class="body" v-if='!loadingMsg'>
      <BodyHeader/>
      <div class="basicDescription">
        <h4 class='descriptionTitle' tabindex="0">
          A brief description
        </h4>
        <p class='descriptionBody' tabindex="0">
          The equilibrium price is the price at which
           the quantity demanded equals the quantity 
           supplied. It is determined by the intersection
            of the demand and supply curves. A surplus 
            exists if the quantity of a good or service 
            supplied exceeds the quantity demanded at the 
            current price; it causes downward pressure on price.
        </p>
      </div>
      <TextExpander
        headerText='More details here'
        :bodyText='expanderBodyText'
      />
      <div class='imgSection'>
        <div class="graphImgWrapper">
          <img 
            src="https://cdn.kastatic.org/ka-perseus-images/63f47bb804ff4c50a60f967b7b29acdfd5fd450a.jpg" 
            alt="graph showing pricing equilibrium." 
          >
        </div>
        <p tabindex="0">
          The demand curve, D, and the supply curve, S, 
          intersect at the equilibrium point E, with an 
          equilibrium price of 1.4 dollars and an equilibrium 
          quantity of 600. The equilibrium is the only price
           where quantity demanded is equal to quantity supplied. 
           At a price above equilibrium, like 1.8 dollars, 
           quantity supplied exceeds the quantity demanded,
            so there is excess supply. At a price below equilibrium,
            such as 1.2 dollars, quantity demanded exceeds 
            quantity supplied, so there is excess demand.
        </p>
      </div>
      <Graph/>
      <div class="priceBtnSection">
        <h4 class='descriptionTitle' tabindex="0">
          Let's try with a real product:
        </h4>
        <p tabindex='0'>
          Below are varying prices for a pair of sunglasses from a real online retailer.
          One of these prices has allowed the sunglasses to sell the most. Can you guess
          which price is at equilibrium?
        </p>
        <div class='priceBtnCont'>
          <button 
          @click='handlePriceBtnClick(idx)'
            class='priceBtn'
            v-for='(btn, idx) in createPriceBtnArr' 
            :key='idx' 
            :value='btn'
            type='button'
          >
            ${{ btn }}
          </button>
        </div>
        <p tabindex='0'>
          Units Sold: {{ consumption }}
        </p>
        <p tabindex='0'>
          Total Revenue: ${{ revenue }}
        </p>
        <transition name='fadeIn'>
          <p v-if='priceBtnMsg' tabindex='0'>
            {{ priceBtnMsg }}
          </p>
        </transition>
      </div>

    </div>

  </div>
</template>





<script>
  import Graph from './components/Graph.vue';
  import Header from './components/Header.vue';
  import TextExpander from './components/TextExpander.vue';
  import BodyHeader from './components/BodyHeader.vue'



  export default {
    name: 'App',



    data() {
      return {
        expanderBodyText: [
          "An increase in demand, all other things unchanged, will cause the equilibrium price to rise; quantity supplied will increase. A decrease in demand will cause the equilibrium price to fall; quantity supplied will decrease.",
          "An increase in supply, all other things unchanged, will cause the equilibrium price to fall; quantity demanded will increase. A decrease in supply will cause the equilibrium price to rise; quantity demanded will decrease.",
          "To determine what happens to equilibrium price and equilibrium quantity when both the supply and demand curves shift, you must know in which direction each of the curves shifts and the extent to which each curve shifts."
        ],
        loadingMsg: null,
        consumption: 0,
        revenue: 0,
        priceBtnMsg: '',
        itemPrice: null,
        selectedPrice: null,
        priceMultiplier: [
          {

            value: 1,
            selected: false
          },
          {

            value: 2,
            selected: false
          },
          {

            value: 3,
            selected: false
          },
          {
  
            value: 4,
            selected: false
          },
          {
  
            value: 5,
            selected: false
          },
          {
            value: 6,
            selected: false
          },
          {
  
            value: 10,
            selected: false
          },
          {
  
            value: 12,
            selected: false
          },
        ]
      }
    },


    
    components: {
      Graph,
      Header,
      TextExpander,
      BodyHeader,
    },



    computed: {
      createPriceBtnArr: function() {
        const price = this.itemPrice;
        let btnPriceArr = this.priceMultiplier.map(b => (b.value * price).toFixed(2));
        return btnPriceArr;
      }
    },



    methods: {
      calculateOutput: function() {
        let Mdemand = -1000;
        let Bdemand = 10000;
        let Msupply = 0; // what if ABC can hire more people when price goes up? 
        let Bsupply = 8000;
        let consumption;
        let supply;
        let message;
        let price = this.selectedPrice;

        consumption = price * Mdemand + Bdemand;
        supply = price * Msupply + Bsupply;

        if (consumption >= supply) {
          consumption = supply;
          message = "The retailer cannot make enough glasses for the demand.";
        }

        if (consumption <= 0) {
          consumption = 0;
          message = "Price too high, no one will buy glasses at this price."
        }

        const revenue = consumption * price;

        this.consumption = consumption;
        this.revenue = revenue;
        this.priceBtnMsg = message ? message : 'At this price, supply and demand are close';
      },



      handlePriceBtnClick: function(idx) {
        for (let i = 0; i < this.priceMultiplier.length; i++) {
          if(i == idx) {
            this.priceMultiplier[i].selected = true;
            this.selectedPrice = this.itemPrice * this.priceMultiplier[i].value;
          }

          this.priceMultiplier[i].selected = false;
        }

        this.calculateOutput()
      },



      checkLocalStorage: function(key) {
        const data = JSON.parse(localStorage.getItem(key));
        let  now = new Date();
        now = now.getTime();

        if(!data) {
          return true;
        }
        if(JSON.parse(data.expire) > now) {
          //if token is expired, delete old data
          localStorage.removeItem(key);
          return true;
        }

        return false;
      },



      createExpirationTime: function() {
      // sets expiration of localStorage token to 1 day to prevent lots of repeat API calls.
        let now = new Date()
        return now.getTime() + 86400;
      },



      getInitData: async function() {
        const domainUrl = process.env.VUE_APP_BASE_URL ? process.env.VUE_APP_BASE_URL : 'https://api.rainforestapi.com/request?'
        const apiKey = process.env.VUE_APP_API_KEY ? process.env.VUE_APP_API_KEY : '48261E1FB0614699BC1D28D2C740DFD3'
        const amazonAsin = 'B06WLLJSN7';
        const url = encodeURI(`${domainUrl}api_key=${apiKey}&type=product&asin=${amazonAsin}&amazon_domain=amazon.com`);
        this.loadingMsg = "Fetching data, please wait."

      await fetch(url, {
        method: 'GET',
        headers: {
          'Content-type': 'application/json'
        }
      })
        .then(response => response.json())
        .then(data => {
          const expiration = this.createExpirationTime();
          const dataObj = {
            value: data,
            expire: expiration,
          }
            localStorage.setItem('priceData', JSON.stringify(dataObj))
            this.setPriceData()
            this.loadingMsg = "Fetching data, please wait."

          })
        .catch((error) => {
          console.error('Error:', error);
          this.errorMsg = 'Unable to get pricing data, so we will use placeholder data.'
        })

      },



      setPriceData: function() {
        //get item price and set data value to it, but if the price isn't there, use 15.00 instead as placeholder

        // const data = JSON.parse(localStorage.getItem('priceData'));
        // const price = data.value.product.buybox_winner.price.value;

        // this.itemPrice = price ? price : 15.00;
        this.itemPrice = 1
      }
    },



    mounted() {
      if(this.checkLocalStorage('priceData')){
        this.getInitData()
      } else {
        this.setPriceData();
      }

    }
  }
</script>





<style>
  :root {
    --clr-darkBg: #555;
    --clr-accent: #26a7c4;
  }

  *,
  *::before,
  *::after {
    box-sizing: border-box;
    padding: 0;
    margin: 0;
    font-family: 'nunito', sans-serif;
  }

  p {
    color: rgb(105, 105, 105);
    font-size: .9rem;
    line-height: 1.4em;
    margin-bottom: 1em;
  }

  img {
    max-width: 100%;
    display: block;
  }

  #app {
    position: relative;
  }

  .loadingMsg {
    padding: 2rem 0;
    margin: 0 auto;
  }

  .body {
    max-width: 50rem;
    margin: 0 auto;
    padding: .5rem .75rem;
  }

  .descriptionTitle {
    color: var(--clr-darkBg);
    font-weight: 600;
    margin-bottom: .5rem;
  }

  .graphImgWrapper {
    border: 1px solid rgba(0, 0, 0, 0.425);
    border-radius: 5px;
    width: 100%;
    padding: .5rem;
    margin-bottom: 1rem;
    margin-top: 1rem;
    overflow: hidden;
    max-width: 400px;
  }

  .priceBtnSection {
    padding: 2rem 0;
  }

  .priceBtnCont {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    margin-bottom: 1rem;
  }

  .priceBtn {
    background-color: #fff;
    border: 2px solid var(--clr-accent);
    color: var(--clr-accent);
    font-size: .9rem;
    padding: .25em .75em;
    margin: .5em;
    cursor: pointer;
    transition: all .2s ease;
  }
  .priceBtn:hover,
  .priceBtn:focus {
    background-color: var(--clr-accent);
    color: #fff;
  }
  
  .fadeIn-enter-active,
  .fadeIn-leave-active {
    opacity: 1;
  }

  .fadeIn-enter-from,
  .fadeIn-leave-to {
    opacity: 0;
  }

  @media only screen and (min-width: 600px) {
    p {
      font-size: 1rem;
      line-height: 1.5em;
    }
  }

  @media only screen and (min-width: 900px) {
    .imgSection {
      display: flex;
      margin: 2rem 0 1rem 0;
    }

    .graphImgWrapper {
      margin-bottom: 0;
      margin-top: 0;
      min-width: 400px;
      margin-right: 1.5rem;
    }

    .imgSection > p {
      max-width: 50%;
    }

  }

</style>
