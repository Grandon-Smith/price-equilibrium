<template>
  <div id="app">
    <Header/>
    <div class="body">
      <BodyHeader/>
      <div class="basicDescription">
        <p class='descriptionTitle' tabindex="0">
          A brief description
        </p>
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
          <img src="https://cdn.kastatic.org/ka-perseus-images/63f47bb804ff4c50a60f967b7b29acdfd5fd450a.jpg" alt="graph showing pricing equilibrium." tabindex="0">
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
      ]
    }
  },


  
  components: {
    Graph,
    Header,
    TextExpander,
    BodyHeader,
  },
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
