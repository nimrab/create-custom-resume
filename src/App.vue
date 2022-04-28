<template>

  <div class="loader-bg" v-if="isLoading">
    <div class="loader"></div>
  </div>
  <div class="container column">


    <AddFormMain
        @createItem="createItem"
        :isLoading="isLoading"
    />
    <ResumeMain
        :dataArray="dataArray"
        @deleteItem="deleteItem"
    />


  </div>
  <CommentsMain
      :commentsArray="commentsArray"
      :areCommentsLoaded="areCommentsLoaded"
      @getComments="getComments"
  />

</template>

<script>
import AddFormMain from "@/components/AddFormMain/AddFormMain";
import ResumeMain from "@/components/ResumeMain/ResumeMain";
import CommentsMain from "@/components/CommentsMain/CommentsMain";

export default {
  components: {CommentsMain, ResumeMain, AddFormMain},
  data() {
    return {
      dataArray: [],
      isLoading: true,
      commentsArray: [],
      areCommentsLoaded: false
    }
  },
  methods: {
    async createItem(newItem) {
      try {
        this.isLoading = true
        await fetch('https://vue-http-1a70e-default-rtdb.asia-southeast1.firebasedatabase.app/block-data.json', {
          method: 'POST',
          mode: 'no-cors',
          headers: {'Content-Type': 'application/json'},
          body: JSON.stringify(newItem)
        })
        await this.getItems()
      } catch (e) {
        console.log(e)
      } finally {
        this.isLoading = false
      }
    },
    async getItems() {
      try {
        this.isLoading = true
        const response = await fetch('https://vue-http-1a70e-default-rtdb.asia-southeast1.firebasedatabase.app/block-data.json')
        const data = await response.json()
        if (!data) return
        const newArr = []
        Object.keys(data).forEach(el => {
          newArr.push({id: el, ...data[el]})
          this.dataArray = newArr
        })
      } catch (e) {
        console.log(e)
      } finally {
        this.isLoading = false
      }
    },

    async deleteItem(id) {
      try {
        this.isLoading = true
        await fetch('https://vue-http-1a70e-default-rtdb.asia-southeast1.firebasedatabase.app/block-data/' + id, {
          method: 'DELETE',
          mode: 'no-cors',
        })
      } catch (e) {
        console.log(e)
      } finally {
        this.isLoading = false
      }
    },
    async getComments() {
      try {
        this.isLoading = true
        const response = await fetch('https://jsonplaceholder.typicode.com/comments?_limit=42')
        const data = await response.json()
        if (!data) return
          this.commentsArray = data.map(el => ({id:el.id, email: el.email, body: el.body}))
          this.areCommentsLoaded = true
      } catch (e) {
        console.log(e)
      } finally {
        this.isLoading = false
      }
    }

  },
  mounted() {
    this.getItems()

    this.emitter.on('deleteItem', data => {
      this.deleteItem(data)
    })
  },


}
</script>

<style>
@import './theme.css';

.avatar {
  display: flex;
  justify-content: center;
}

.avatar img {
  width: 150px;
  height: auto;
  border-radius: 50%;
}
</style>
