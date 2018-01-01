<template>
  <div id="app">
    <v-header ></v-header>
    <div class="tab">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>


      </div>
      <div class="tab-item">
        <router-link to="/rating">评论</router-link>


      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>


      </div>
    </div>
    <router-view ></router-view>

  </div>
</template>

<script type="text/ecmascript-6">
  import vheader from './components/header/header.vue'

  export default {
    name: 'app',
    data () {
      return {
        seller: {}

      }
    },
    created () {
      // this.$http.get('./data.json')
      //   .then((response) => {
      //     console.log(response)
      //       this.seller = response.body.seller
      //   })
    },

    components: {
      'v-header': vheader
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "./common/stylus/mixin.styl"

  #app
    .tab
      display: flex
      width: 100%
      height: 40px
      line-height: 40px
      border-1px(rgba(7, 17, 27, 0.1))
      .tab-item
        flex: 1
        text-align center
        & > a
          display: block
          font-size: 14px
          color: rgb(77, 85, 93)
          &.router-link-active
           color: rgb(240, 20, 20)




</style>
