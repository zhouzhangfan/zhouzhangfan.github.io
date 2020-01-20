<template>
  <div class="page">
    <Header show></Header>
    <div class="title">{{title}}</div>
    <Content class="content" />
  </div>
</template>

<script>
import Header from '@theme/components/Header.vue'
import '@theme/style/content.less' 
export default {
  components: { Header },
  computed: {
    title () {
      const { title } = this.$page
      return title
    }
  },
  mounted () {
    console.log(this.$page)
  }
}
</script>

<style lang="less" scoped>
@headerHeight: 12vw;
.page{
  padding-top: @headerHeight + 5vw;
  .title{
    font-size: 6vw;
    font-weight: bold;
    margin: 3vw 0;
    padding: 0 5vw;
  }
}
</style>
