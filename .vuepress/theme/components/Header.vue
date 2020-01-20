<template>
  <div class="header-fixed" :class="{'show': show}">
    <div class="avatar" :style="`background-image:url('${avatar}')`"></div>
    <div class="title">{{title}}</div>
  </div>
</template>

<script>
export default {
  props: {
    show: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    avatar () {
      const { themeConfig } = this.$site
      return themeConfig.avatar
    },
    title () {
      const { title } = this.$site
      return title
    }
  }
}
</script>

<style lang="less" scoped>
@fontcolor: #4d4d4d;
@headerHeight: 12vw;
.header-fixed{
  position: fixed;
  top: -@headerHeight;
  left: 0;
  right: 0;
  height: @headerHeight;
  background-color: #fff;
  border-bottom: 1px solid #f5f5f5;
  transition: top 600ms;
  .avatar{
    border-radius: 50%;
    height: 8vw;
    width: 8vw;
    overflow: hidden;
    background-position: center center;
    background-size: cover;
    float: left;
    margin: 2vw 0 0 2vw;
  }
  .title{
    font-size: 4vw;
    font-weight: bold;
    line-height: @headerHeight;
    float: right;
    margin-right: 5vw;
    color: @fontcolor;
  }
}
.header-fixed.show{
  top: 0;
}
</style>
