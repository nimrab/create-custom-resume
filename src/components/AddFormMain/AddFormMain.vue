<template>
  <form class="card card-w30">
    <SelectForm
        :options="formData.options"
        v-model="formData.selected"
    />
    <TextArea
        v-model.trim="formData.textAreaValue"
    />
    <button
        class="btn primary"
        :disabled="isError"
        @click.prevent="sendItem"
    >Добавить
    </button>
  </form>
</template>

<script>
import SelectForm from "@/components/AddFormMain/SelectForm";
import TextArea from "@/components/AddFormMain/TextArea";

export default {
  components: {TextArea, SelectForm},
  emits: ['createItem'],
  props: {
    isLoading: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      formData: {
        selected: 'title',
        options: [
          {title: 'Заголовок', value: 'title'},
          {title: 'Подзаголовок', value: 'subtitle'},
          {title: 'Аватар', value: 'avatar'},
          {title: 'Текст', value: 'text'},
        ],
        textAreaValue: ''
      },
      error: {
        minLength: 4,
        maxLength: 1000
      }
    }
  },
  computed: {
    isError() {
      return (
          this.formData.textAreaValue.length < this.error.minLength ||
          this.formData.textAreaValue.length > this.error.maxLength)
    }
  },
  methods: {
    sendItem() {
      if (!this.isLoading) {
        this.$emit('createItem', {header: this.formData.selected, body: this.formData.textAreaValue})
        this.formData.selected = 'title'
        this.formData.textAreaValue = ''
      }
    }
  }

}


</script>

<style scoped>

</style>