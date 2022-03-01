<template>
  <section>
    <div class='expandableTextBox'>
      <h3>
        {{ headerText }}
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


</style>
