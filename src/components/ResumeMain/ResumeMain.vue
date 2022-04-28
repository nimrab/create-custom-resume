<template>

  <div class="card card-w70">

    <EmptyBlock v-if="!dataArray.length"/>
    <component
        v-else
        v-for="item in dataArray"
        :is="receiveComponentName(item)"
        :body="item.body"
        :id="item.id"
        :key="item.id"
    />
  </div>

</template>

<script>
import TitleBlock from "@/components/ResumeMain/TitleBlock";
import AvatarBlock from "@/components/ResumeMain/AvatarBlock";
import SubTitleBlock from "@/components/ResumeMain/SubTitleBlock";
import TextBlock from "@/components/ResumeMain/TextBlock";
import EmptyBlock from "@/components/ResumeMain/EmptyBlock";

export default {
  components: {EmptyBlock, TextBlock, SubTitleBlock, AvatarBlock, TitleBlock},
  props: {
    dataArray: {
      type: Array,
      required: true
    }
  },

  methods: {
    receiveComponentName(arrItem) {
      switch (arrItem.header) {
        case 'title':
          return 'TitleBlock'
        case 'subtitle':
          return 'SubTitleBlock'
        case 'avatar':
          return 'AvatarBlock'
        case 'text':
          return 'TextBlock'
      }
    }
  },
}
</script>

<style scoped>

</style>