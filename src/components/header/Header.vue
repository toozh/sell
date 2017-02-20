<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img :src="seller.avatar" width="64px" height="64px"/>
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="desc">
          {{seller.description}}
        </div>
        <div v-if="seller.supports" class="supports">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
    </div>
    <div class="bulletin-wrapper">
      <span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>

  </div>
</template>

<script type="text/ecmascript-6">
  export default {
    name: 'header',
    data () {
      return {
        classMap: ['decrease', 'discount', 'special', 'invoice', 'guarantee']
      };
    },
    props: {
      seller: {
        type: Object
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/main.styl";

  .header
    background-color: #000
    .content-wrapper
      padding: 24px 24px
      font-size: 0
      .avatar
        display: inline-block
        width: 64px
        height: 64px
        img
          border-radius: 4px
      .content
        display: inline-block
        vertical-align: top
        margin-left: 16px
        .title
          margin-top: 2px
          vertical-align: top
          .brand
            display: inline-block
            width: 30px
            height: 18px
            bg-image('brand')
            background-size: 30px 18px
            background-repeat: no-repeat
          .name
            vertical-align: top
            margin-left: 6px
            color: rgb(255, 255, 255)
            font-size: 16px
            font-weight: bold
        .desc
          margin-bottom: 10px
          font-size: 12px
          color: rgb(255, 255, 255)
          line-height: 24px
        .supports
          .icon
            display: inline-block
            vertical-align: top
            width: 12px
            height: 12px
            margin-right: 4px
            background-size: 12px 12px
            background-repeat: no-repeat
            &.decrease
              bg-image('decrease_1')
            &.discount
              bg-image('discount_1')
            &.special
              bg-image('special_1')
            &.invoice
              bg-image('invoice_1')
            &.guarantee
              bg-image('guarantee_1')
          .text
            font-size: 10px
            color: rgb(255, 255, 255)
            font-weight: 200
    .bulletin-wrapper
      .bulletin-title
        background-size: 18px 12px
        background-repeat: no-repeat
        bg-image('bulletin')
</style>
