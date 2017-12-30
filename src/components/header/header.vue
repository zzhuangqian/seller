<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avart">
        <img alt="" width="64" height="64">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">名称</span>
        </div>
        <div class="description">
          蜂鸟配送/48分钟送达
        </div>
        <div class="support">
          <span class="icon">tupian</span>
        </div>

      </div>
    </div>
    <div class="bulletin-wrapper">
      <span class="bulletin-title">
        gonggao
      </span>
      <span class="bulletin-text">
        sdfasdfa
      </span>
      <i>jiantou</i>
    </div>
    <div class="detail">
      <div class="detail-wrapper">
        <div class="detail-main">
          <h1 class="name">商家名</h1>
          <div class="star-wrapper">
            <star :size="48" :score="2.5"></star>
          </div>
          <div class="title">
            <div class="line"></div>
            <div class="text">优惠信息</div>
            <div class="line"></div>
          </div>
          <!--<ul v-if="seller.supports" class="supports">-->
            <!--<li class="support-item" v-for="item in seller.supports">-->
              <!--<span class="icon" :class="classMap[seller.supports[$index].type]"></span>-->
              <!--<span class="text">{{seller.supports[$index].description}}</span>-->
            <!--</li>-->
          <!--</ul>-->
          <div class="title">
            <div class="line"></div>
            <div class="text">商家公告</div>
            <div class="line"></div>
          </div>
          <div class="bulletin">
            <!--<p class="content">{{seller.bulletin}}</p>-->
          </div>
        </div>
      </div>
      <div class="detail-close">
        <i>close</i>
      </div>
    </div>
  </div>

</template>

<script type="text/ecmascript-6">
  import star from 'components/star/star'
  export default {
    name: 'vheader',
    props: {
      type: Object
    },
    components: {
      'star': star
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl"
  .header
    color: #fff
    background: rgba(7, 17, 27, 0.5)
    .content-wrapper
      padding: 24px 12px 18px 24px
      font-size: 0px
      .avart
        display: inline-block
        vertical-align: top
      .content
        display: inline-block
        font-size: 14px
        margin-left: 16px
        .title
          margin: 2px 0 8px 0
          .brand
            display: inline-block
            width: 30px
            height: 18px
            background: yellow
            vertical-align: top

            background-size: 30px 18px
            background-repeat: no-repeat
          .name
            margin-left: 6px
            font-size: 16px
            line-height: 18px
            fonfont-weight: 400
        .description
          margin-bottom: 10px
          line-height: 12px
          font-size: 12px
        .support
          .icon
            display: inline-block
            width: 12px
            height: 12px
            margin-right: 4px
            background-size: 12px 12px
            background-repeat : no-repeat



    .bulletin-wrapper
      height: 28px
      line-height: 28px
      padding:0 22px 0 22px
      white-space: nowrap
      overflow: hidden
      text-overflow: ellipsis
      .bulletin-title
        display: inline-block
        width: 22px
        height: 12px
        background: pink
        background-size : 22px 12px
        background-repeat:no-repeat
    .detail
      position: fixed
      z-index: 100
      top: 0
      left: 0
      width: 100%
      height: 100%
      overflow: hidden
      background: blue
      .detail-wrapper
        width: 100%
        min-height: 100%
        .detail-main
          padding-top: 64px
          padding-bottom: 64px
          .name
            line-height: 16px
            text-align: center
            font-size: 16px
          .star-wrapper
            margin-top:18px
            text-align: center
            padding:2px 0
          .title
            display: flex
            width: 80%
            margin:30px auto 24px auto
            .line
              flex: 1
              position: relative
              top: -6px
              border-bottom:1px solid rgba(255,255,255,0.3)
            .text
              padding: 0 12px
              font-weight: 700
              font-size: 14px

      .detail-close
        position: relative
        width: 32px
        height: 32px
        margin: -64px auto 0 auto
        clear: both
        font-size: 32px


</style>
