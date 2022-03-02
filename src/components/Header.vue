<template>
  <div class='headerContainer'>
    <div class='headerWrapper'>
      <h1>
        Economic Principles
      </h1>

    </div>
    
  </div>
</template>




<script>
  export default {

    name: 'app-header',

  }

</script>




<style scoped>
  .headerContainer {
    /* background-color: var(--clr-darkBg); */
    background: url('https://www.conncoll.edu/media/major-images/Economics.jpg');
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    font-family: 'Courier New', Courier, monospace;
    color: #fff;
    position: sticky;
    top: 0;
    left: 0;
    right: 0;
    padding: 1.5rem .75rem 1.5rem 0;
    display: flex;
    justify-content: space-between;
  }

  h1 {
    font-size: 1.7rem;
    padding: .2em .5em .2em .5em;
  }

</style>
