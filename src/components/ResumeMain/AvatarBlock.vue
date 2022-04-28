<template>
  <div class="avatar">
    <img :src="body">
  </div>
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