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
          <span>tupian</span>
        </div>

      </div>
    </div>
    <div class="bulletin-wrapper"></div>
  </div>

</template>

<script type="text/ecmascript-6">
  export default {
    name: 'vheader',
    props: {
      type: Object
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .header
     color: #fff
     background: #000
     .content-wrapper
      padding; 24px 12px 18px 24px
      .avart
        display; inline-block
      .content
        display; inline-block
</style>
