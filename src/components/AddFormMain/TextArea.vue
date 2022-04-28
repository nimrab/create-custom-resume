<template>
  <div class="form-control">
    <label>Значение</label>
    <textarea
        rows="3"
        :value="modelValue"
        @input="onChange"
    />
  </div>
</template>

<script>
export default {
  emits: ['update:modelValue'],
  props: {
    modelValue: String,
  },
  methods: {
    onChange($event) {
      this.$emit('update:modelValue', $event.target.value)
    }
  }
}
</script>

<style scoped>

</style>