<template>
  <div class="section-wrapper">
    <h1 @dblclick="deleteItem">
      {{ body }}
    </h1>
  </div>

</template>

<script>

export default {
  components: {},
  props: {
    body: {
      type: String,
      required: true
    },
    id: {
      type: String,
      required: true
    }
  },
  data() {
    return {
    }
  },
  methods: {
    deleteItem() {
      this.emitter.emit('deleteItem', this.id)
    }
  }
}
</script>

<style scoped>

</style>