<template>
  <section>
    <div 
      class='expandableTextBox'
      :class='{ expanded : expandText }'
    >
      <button @click='expandText = !expandText' type='button'>
        <h3>
          {{ headerText }}
        </h3>
        <font-awesome-icon class='svg' icon='fa-solid fa-circle-info'/>
      </button>
      <div>
        <p v-for='(content, idx) in bodyText' :key='idx' class='expandBodyPara'>
          {{ content }}
        </p>

      </div>
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
      type: Array,
      required: false,
    },

  }
}
</script>




<style scoped>
h3 {
  color: var(--clr-accent);
  font-size: 1.2rem;
}

button {
  background-color: transparent;
  border: none;
  color: var(--clr-accent);
  width: 100%;
  height: 1.75em;
  margin-bottom: 1rem;
  display: flex;
  justify-content: space-between;
  font-weight: bold;
  cursor: pointer;
}

.expandableTextBox {
  border: 1px solid rgba(0, 0, 0, 0.5);
  border-radius: 5px;
  box-shadow: 0 0 5px rgba(0, 0, 0, .35);
  height: 2.5rem;
  padding: .5rem 1rem;
  margin-bottom: 1.5rem;
  overflow: hidden;
  transition: .2s all ease;
}

.expanded {
  height: 12rem;
  overflow: auto;
}

.svg {
  display: block;
  height: 100%;
  /* width: 100%; */
}

.expandBodyPara {
  font-size: .9rem;
  margin-bottom: .75rem;
  color: rgb(105, 105, 105);
}

</style>
