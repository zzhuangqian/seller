<template>
  <div class="shopcart">
    <div class="content">
      <div class="content-left">
        <div class="log-wrapper">
          <div class="logo" v-bind:class="{'highlight': totalCount>0 } ">
            <i class="icon-shopping_cart"></i>
          </div>
          <div class="num">{{totalCount}}</div>
        </div>
        <div class="price">
          ￥{{totalPrice}}

        </div>
        <div class="desc">另需要配送费元</div>

      </div>
      <div class="content-right">
        <div class="pay" >
          34元
        </div>
        </div>
    </div>
  </div>
</template>
<script type="text/ecmascript-6">
  export default {
    name: 'shopcart',
    props: {
      selectFoods: {
        type: Array,
        default () {
          return []
        }
      }
    },
    computed: {
      totalPrice () {
        let total = 0
        this.selectFoods.forEach((food) => {
          total += food.price * food.count
        })
        return total
      },
      totalCount () {
        let count = 0
        this.selectFoods.forEach((food) => {
          count += food.count
        })
        return count
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .shopcart
    position: fixed
    left: 0
    bottom: 0
    z-index: 50
    width: 100%
    height: 48px
    .content
      display: flex
      background: #141d27
      height: 100%
      font-size:0
      .content-left
        flex:1
        .log-wrapper
          display: inline-block
          position: relative
          top: -10px
          margin:0 12px
          padding: 6px
          width:56px
          height: 56px
          box-sizing:border-box
          vertical-align: top
          border-radius: 50%
          background: red
          .num
            position: absolute
            top: 0
            right: 0
            width: 24px
            height: 16px
            line-height: 16px
            text-align: center
            border-radius: 16px
            box-shadow: 0 4px 8px 0 rgba(0,0,0,0.4)
            background: rgb(240,20 ,20 )
            color: white
            font-size:12px
          .logo
            width: 100%
            height: 100%
            border-radius: 50%
            background: #2b343c
            &.highlight
              background: rgb(0,160,255)
            .icon-shopping_cart
              line-height: 44px
              font-size: 24px
              color: #80858a
        .price
          display: inline-block
          vertical-align: top
          line-height: 24px
          margin-top: 12px
          box-sizing : border-box
          padding-right:12px
          border-right:1px solid rgba(255,255,255,0.1)
          font-size: 16px
          font-weight: 700
          color: pink
        .desc
          display: inline-block
          vertical-align: top
          margin:12px 0 0 12px
          line-height: 24px
          color: yellow
          font-size:10px

      .content-right
        flex: 0 0 105px
        width: 105px
        .pay
          height: 48px
          line-height: 48px
          text-align: center
          font-size: 12px
          font-weight: 700



</style>
