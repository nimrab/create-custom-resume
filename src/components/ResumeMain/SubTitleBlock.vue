<template>
  <h2>{{ this.body }}</h2>
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