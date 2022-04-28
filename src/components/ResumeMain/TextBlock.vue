<template>
  <p>{{this.body}}</p>
</template>

<script>
export default {
  props: {
    body: {
      type: String,
      required: true
    }
  }
}
</script>

<style scoped>

</style>