<template>
  <div class="form-control">
    <label>Тип блока</label>
    <select @change="onChange">
      <option
          v-for="(item, idx) in options"
          :value="item.value"
          :selected="item.value === modelValue"
          :key="idx"
      >{{ item.title }}</option>
    </select>
  </div>
</template>

<script>
export default {
  emits: ['update:modelValue'],
  props: {
    modelValue: String,
    options: Array,
  },
  methods: {
    onChange($event) {
      this.$emit('update:modelValue', $event.target.value)
    }
  },

}
</script>

<style scoped>

</style>