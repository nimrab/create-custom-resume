<template>
  <div class="container">
    <p>
      <button
          class="btn primary"
          v-if="!areCommentsLoaded"
          @click="getComments"
      >Загрузить комментарии</button>
    </p>
    <div class="card">
      <h2>Комментарии</h2>
      <ul class="list">
        <li
            class="list-item"
            v-for="item in commentsArray"
            :key="item.id"
        >
          <div>
            <p><strong>{{ item.email }}</strong></p>
            <small>{{ item.body }}</small>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    commentsArray: {
      type: Array,
      required: true
    },
    areCommentsLoaded: {
      type: Boolean,
      required: true
    }
  },
  methods: {
    getComments() {
      this.$emit('getComments')
    }
  }
}
</script>

<style scoped>

</style>