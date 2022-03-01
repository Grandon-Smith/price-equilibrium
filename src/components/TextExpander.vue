<template>
  <section>
    <div 
      class='expandableTextBox'
      :class='{ expanded : expandText }'>
      <h3>
        {{ headerText }}
        <button @click='expandText = !expandText'>
          i
        </button>
      </h3>
      <p>
        {{ bodyText }}
      </p>
    </div>
  </section>
</template>




<script>
export default {
  name: 'text-expansion',



  data() {
    return {
      expandText: false,
    }
  },




  props: {
    headerText: {
      type: String,
      required: false,
    },
    bodyText: {
      type: String,
      required: false,
    },

  }
}
</script>




<style scoped>
h3 {
  padding-bottom: 1rem;
  display: flex;
  justify-content: space-between;
}

button {
  background-color: #fff;
  border: 1px solid green;
  border-radius: 50%;
  color: green;
  width: 1.75em;
  height: 1.75em;
  font-weight: bold;
  cursor: pointer;
}

.expandableTextBox {
  border: 1px solid rgba(0, 0, 0, 0.5);
  border-radius: 5px;
  overflow: hidden;
  padding: .5rem 1rem;
  height: 2.5rem;
  transition: .2s all ease;
}

.expanded {
  height: 10rem;
  overflow: auto;
}

</style>
