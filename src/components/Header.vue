<template>
  <header>
    <h1>
      Price Equilibrium
    </h1>
    <div class='headerImgWrapper'>

    </div>
  </header>
</template>




<script>
  export default {

    name: 'header',



    props: {
    }
  }

</script>




<style scoped>
  header {
    background-color: var(--clr-darkBg);
    font-family: 'Courier New', Courier, monospace;
    color: #fff;
    position: sticky;
    top: 0;
    left: 0;
    right: 0;
    padding: .5rem;
    display: flex;
    justify-content: space-between;
  }

  h1 {
    font-size: 1.7rem;
  }

  .headerImgWrapper{
    background-color: #fff;
    width: 1.8rem;
    height: 1.8rem;
  }

</style>
