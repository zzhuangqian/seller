<template>
  <div class="cartcontrol">
    <transition name="move">
    <div class="cart-decrease" @click="decrease" v-show="food.count > 0" >
      <span class="inner">-</span>
    </div>
      </transition>
    <div class="cart-count" v-show="food.count > 0">{{food.count}}</div>
    <div class="cart-add" @click="addCart">+</div>
  </div>

</template>

<script type="text/ecmascript-6">
  import vue from 'vue'
  export default {
    name: 'cartcontrol',
    props: {
      food: {
        type: Object
      }
    },
    created () {

    },
    methods: {
      addCart (event) {
        if (!event._constructed) {
            return
        }
        if (!this.food.count) {
          vue.set(this.food, 'count', 1)
        } else {
          this.food.count ++
        }
        this.$emit('add', event.target)
      },
      decrease (event) {
        if (!event._constructed) {
          return
        }
        this.food.count --
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .cartcontrol
    font-size: 0
    .cart-decrease
      display: inline-block
      padding: 6px
      opacity: 1
      transform: translate3d(0, 0, 0)
      .inner
        display: inline-block
        line-height: 24px
        font-size: 24px
        color: rgb(0, 160, 220)
        transition: all 0.4s linear
        transform: rotate(0)
      &.move-enter-active, &.move-leave-active
        transition: all 0.4s linear
      &.move-enter, &.move-leave-active
        opacity: 0
        transform: translate3d(24px, 0, 0)
        .inner
          transform: rotate(180deg)

    .cart-count
      display: inline-block
      font-size:14px
      width: 15px
      text-align: center
    .cart-add
      display: inline-block
      font-size: 14px
      padding:6px
      background: lightcoral


</style>
