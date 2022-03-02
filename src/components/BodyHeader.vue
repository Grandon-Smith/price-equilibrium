<template>
  <div class="bodyHeader">
    <h2>
      Price Equilibrium
    </h2>
    <p>
      Learn about the economics of supply and demand.
    </p>
    <div class='tagsContainer'>
      <span 
        class='subjectTag' 
        v-for='(tag, idx) in tags' 
        :key='idx'
      >
      {{ tag }}
      </span>
    </div>
    <div class='dividerBar'></div>
  </div>
</template>

<script>



export default {
  name: 'page-data',





  data() {
    return {
       tags: [
        'Economics',
        'Marketing',
        'Finance',
      ]
    }
  },




  
  components: {
  
  },


  methods: {
    
  },


}
</script>



<style scoped>
  h2 {
    font-size: 1.4rem;
    padding: .5em 0;
    color: var(--clr-darkBg);
  }

  .bodyHeader {
    margin: .75rem 0;
  }

  p {
    /* color: var(--clr-accent); */
    color: rgb(105, 105, 105);
    padding:  0 0 .75rem 0;
  }

  .tagsContainer {
    display: flex;
    justify-content: flex-start;
  }

  .subjectTag {
    background-color: rgb(219, 219, 219);
    color: rgb(105, 105, 105);
    padding: .2em .5em;
    margin-right: .5em;
    border-radius: 4px;
    font-size: .9rem;
  }

  .dividerBar {
    height: 1px;
    width: 90%;
    margin: 1.5rem auto;
    background-color: rgb(160, 160, 160);
  }

</style>
