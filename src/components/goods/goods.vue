<template>
  <div class="goods">
    <div class="menu-wrapper" ref="menuWrapper">
    <ul>
      <li v-for="(item ,index ) in goods" class="menu-item" v-bind:class="{'current': currentIndex === index}"  @click="selectMenu(index,$event)">
        <span class="text">
          <span v-show="item.type>0" class="icon" :class="classMap[item.type]" ></span>
          {{item.name}}{{index}}</span>
      </li>
    </ul>
    </div>
    <div class="foods-wrapper"  ref="foodsWrapper" >
      <ul>
        <li v-for="item in goods" class="food-list food-list-hook" >
          <h1 class="title">{{item.name}}</h1>
          <ul>
            <li v-for="food in item.foods" class="food-item border-1px">
              <div class="icon">
                <img width="57px" :src="food.icon" alt="">
              </div>
              <div class="content">
                <h2 class="name">
                  {{food.name}}
                </h2>
                <p class="desc">{{food.description}}</p>
                <div class="extra">
                  <span>乐手{{food.sellCount}}份</span>
                  <span>好评率{{food.rating}}%</span>
                </div>
                <div class="price">
                  <span class="now">￥{{food.price}}</span>
                  <span class="old" v-show="food.oldPrice">￥{{food.oldPrice}}</span>
                </div>
                <div class="cartcontrol-wrapper">
                  <cartcontrol @add="addFood"  :food="food" ></cartcontrol>
                </div>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
    <shopcart ref="shopcart"  v-if="seller" :selectFoods="selectFoods" :deliveryPrice="seller.deliveryPrice" :minPrice="seller.minPrice"></shopcart>

  </div>
</template>

<script type="text/ecmascript-6">
  import BScroll from 'better-scroll'
  import shopcart from 'components/shopcart/shopcart.vue'
  import cartcontrol from 'components/cartcontrol/cartcontrol.vue'
 export default {
   name: 'goods',
   data () {
     return {
       goods: [],
       listHeight: [],
       scrollY: 0,
       seller: {}
     }
   },
   computed: {
     currentIndex () {
       for (let i = 0; i < this.listHeight.length; i++) {
         let height1 = this.listHeight[i]
         let height2 = this.listHeight[i + 1]
         if (!height2 || (this.scrollY >= height1 && this.scrollY < height2)) {
           return i
         }
       }
     },
     selectFoods () {
       let foods = []
       this.goods.forEach((good) => {
        good.foods.forEach((food) => {
          if (food.count) {
            foods.push(food)
          }
        })
       })
       return foods
     }
   },
   created () {
     this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
     this.$http.get('./data.json').then((response) => {
       console.log(response)
       this.goods = response.body.goods
       this.seller = response.body.seller
       this.$nextTick(() => {
         this._initScroll()
         this._calculateHeight()
       })
     })
   },
   methods: {
     _initScroll () {
       this.menuScroll = new BScroll(this.$refs.menuWrapper, {
         click: true
       })
       this.foodScroll = new BScroll(this.$refs.foodsWrapper, {
         probeType: 3,
         click: true
       })
       this.foodScroll.on('scroll', (pos) => {
         this.scrollY = Math.abs(Math.round(pos.y))
       })
     },
     selectMenu (index, event) {
       if (!event._constructed) {
         return
       }
       let foodList = this.$refs.foodsWrapper.getElementsByClassName('food-list-hook')
       let el = foodList[index]
       this.foodScroll.scrollToElement(el, 300)
     },
     _calculateHeight () {
       let foodList = this.$refs.foodsWrapper.getElementsByClassName('food-list-hook')
       let height = 0
       this.listHeight.push(height)
       for (let i = 0; i < foodList.length; i++) {
         let item = foodList[i]
         height += item.clientHeight
         this.listHeight.push(height)
       }
     },
     addFood (target) {
       this._drop(target)
     },
      _drop (target) {
       this.$nextTick(() => {
         this.$refs.shopcart.drop(target)
       })
      }
   },
   components: {
     shopcart,
     cartcontrol
  }
 }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl"
  .goods
    display: flex
    position: absolute
    top: 174px
    bottom: 46px
    width: 100%
    overflow: hidden
    .menu-wrapper
      flex:0 0 80px
      width: 80px
      background: #f3f5f7
      .menu-item
        display: table
        width: 56px
        height:54px
        line-height:14px
        padding: 0 12px
        border-1px(rgba(7, 17, 27, 0.1))
        &.current
          position: relative
          z-index: 10
          margin-top: -1px
          background: pink
         font-weight: 700
        .icon
          display: inline-block
          vertical-align: top
          width: 12px
          height: 12px
          margin-right: 2px
          background-size: 12px 12px
          background-repeat: no-repeat
          &.decrease
            bg-image('decrease_3')
          &.discount
            bg-image('discount_3')
          &.guarantee
            bg-image('guarantee_3')
          &.invoice
            bg-image('invoice_3')
          &.special
            bg-image('special_3')
        .text
          display: table-cell
          width: 56px
          vertical-align: middle
          font-size: 12px
    .foods-wrapper
      flex: 1
      .title
        padding-left:14px
        height: 26px
        line-height: 26px
        border-left:2px solid #d9dde1
        font-size: 12px
        color: rgb(147,153,159)
        background: #f3f5f7
      .food-item
        display: flex
        margin: 18px
        padding-bottom: 18px
        border-1px(rgba(7, 17, 27, 0.1))
        &:list-child
          border-none()
          margin-bottom: 0
        .icon
          flex:0 0 57px
          margin-right: 10px
        .content
          flex:1
          .name
            margin:2px 0 8px 0
            height: 14px
            line-height: 14px
            font-size: 14px
            color: rgb(7,17,27)
          .desc,.extra

            line-height: 10px
            font-size: 10px
            color: blue
          .desc
            margin-bottom:8px
          .extra
            &.count
              margin-right: 12px
          .price
            font-weight:700
            line-height: 24px
            .now
              color: red
              font-size:14px
              margin-right: 8px
            .old
              color: gray
              font-size:10px
              text-decoration: line-through
          .cartcontrol-wrapper
            position: absolute
            right: 0
            bottom: 2px


</style>
