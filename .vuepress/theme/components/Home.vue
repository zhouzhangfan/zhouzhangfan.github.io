<template>
  <div class="home">
    <div class="header">
      <div class="avatar">
        <div class="pic" :style="`background-image:url('${avatar}')`"></div>
      </div>
      <div class="title">{{title}}</div>
      <div class="description">{{description}}</div>
      <div class="tabs">
        <div class="tab">技术博客</div>
        <div class="tab">日记</div>
      </div>
      <Header :show="showHeader"></Header>
    </div>
    <div ref="pages" class="pages">
      <div class="page" v-for="(page, index) in pages" :key="index" @click="$router.push(page.path)">
        <div class="banner" v-if="page.frontmatter.banner"  :style="`background-image:url('${page.frontmatter.banner}')`"></div>
        <div class="title">{{page.title}}</div>
        <div class="excerpt" v-html="page.excerpt"></div>
      </div>
    </div>
  </div>
</template>

<script>
import Header from '@theme/components/Header.vue'
export default {
  components: { Header },
  data () {
    return {
      showHeader: false
    }
  },
  computed: {
    avatar () {
      const { themeConfig } = this.$site
      return themeConfig.avatar
    },
    title () {
      return this.$page.frontmatter.title
    },
    description () {
      const { description } = this.$site
      return description
    },
    pages () {
      const pages = JSON.parse(JSON.stringify(this.$site.pages))      
      pages.splice(pages.indexOf(pages.find(x => x.title === 'Home')), 1)
      pages.reverse()
      let ret = pages.map(x => Object.assign(x, {
        title: x.frontmatter.title ? x.frontmatter.title : x.path.split('/').pop().split('.html')[0]
      }))
      return ret
    }
  },
  mounted () {
    let that = this
    document.addEventListener('scroll', e => {
      if (that.$refs.pages) {
        that.showHeader = (that.$refs.pages.offsetTop < document.body.scrollTop + e.target.documentElement.scrollTop + 80)
      }
    })
  }
}
</script>

<style lang="less" scoped>
@fontcolor: #4d4d4d;
.home{
  .header{
    margin-bottom: 20vw;
    .avatar{
      border-radius: 50%;
      margin: 10vw auto;
      border: 2px solid @fontcolor;
      padding: 5px;
      width: 30vw;
      height: 30vw;
      .pic{
        border-radius: 50%;
        height: 100%;
        width: 100%;
        overflow: hidden;
        background-position: center center;
        background-size: cover;
      }
    }
    .title{
      text-align: center;
      font-weight: bold;
      font-size: 6vw;
      color: @fontcolor;
    }
    .description{
      margin-top: 5vw;
      text-align: center;
      font-size: 4vw;
      color: @fontcolor;
    }
    .tabs{
      text-align: center;
      margin: 20px auto 0;
      .tab{
        display: inline-block;
      }
    }
  }
  .pages{
    padding: 5vw;
    background-color: #f5f5f5;
    .page{
      color: @fontcolor;
      background-color: #fff;
      margin-bottom: 5vw;
      .banner{
        height: 35vw;
        background-position: center center;
        background-size: cover;
      }
      .title{
        font-size: 5vw;
        font-weight: bold;
        padding: 5vw 4vw 0;
      }
      .excerpt{
        padding: 2vw 4vw;        
      }
    }
  }
}
</style>

<style lang="less">
.excerpt{
  p{
    margin: 1vw 0;
  }      
}
</style>



