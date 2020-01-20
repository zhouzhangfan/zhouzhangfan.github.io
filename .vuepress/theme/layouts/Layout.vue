<template>
  <div class="theme-container">
    <Home v-if="home" />
    <Page v-else />
    <!-- <img :src="avatar" /> -->
  </div>
</template>

<script>
import Home from '@theme/components/Home.vue'
import Page from '@theme/components/Page.vue'
export default {
  components: { Home, Page },
  computed: {
    home () {
      return this.$page.frontmatter.home
    }
  }
}
</script>

<style lang="less">
html, body{
  padding: 0;
  margin: 0;
}
</style>


