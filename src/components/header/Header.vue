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
      <div v-if="seller.supports" class="supports-more" @click="toggleDetails">
        <span>{{seller.supports.length}}个</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div class="bulletin-wrapper">
      <span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="bg">
      <img :src="seller.avatar"/>
    </div>
    <transition name="fade">
      <div v-show="detailsShow" ref="detail" class="details">
        <div class="details-wrapper clearfix">
          <div class="name">{{seller.name}}</div>
          <div class="details-main">
            <div class="title">
              <div class="line"></div>
              <div class="text">优惠信息</div>
              <div class="line"></div>
            </div>
            <div class="supports">
              <ul>
                <li v-for="support in seller.supports"><span class="icon" :class="classMap[support.type]"></span>{{support.description}}</li>
              </ul>
            </div>
            <div class="title">
              <div class="line"></div>
              <div class="text">商家公告</div>
              <div class="line"></div>
            </div>
            <div class="bulletin">
              <p>{{seller.bulletin}}</p>
            </div>
          </div>
        </div>
        <div class="details-close">
          <i class="icon-close" @click="toggleDetails"></i>
        </div>
      </div>
    </transition>

  </div>
</template>

<script type="text/ecmascript-6">

  import BScroll from 'better-scroll';

  export default {
    name: 'header',
    data () {
      return {
        classMap: ['decrease', 'discount', 'special', 'invoice', 'guarantee'],
        detailsShow: false
      };
    },
    created () {

    },
    watch: {
      seller () {
      }
    },
    ready () {
    },
    methods: {
      _initScroll () {
        console.log(this.$refs);
        this.scroll = new BScroll(this.$refs.detail, {
        });
      },
      toggleDetails () {
        this.detailsShow = !this.detailsShow;
      }
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
    position: relative
    width: 100%
    height: 100%
    background-color: rgba(7, 17, 27, 0.5)
    .content-wrapper
      position: relative
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
      .supports-more
        position: absolute
        bottom: 14px
        right: 12px
        height: 24px
        font-size: 10px
        line-height 24px
        border-radius: 14px
        color: rgb(255, 255, 255)
        background-color: rgba(0, 0, 0, 0.2)
        padding: 0px 8px
        text-align: center

    .bulletin-wrapper
      position: relative
      height: 28px
      line-height: 28px
      padding: 0 22px 0 12px
      color: #fff
      white-space: nowrap
      overflow: hidden
      text-overflow: ellipsis
      background: rgba(7, 17, 27, 0.2)
      .bulletin-title
        display: inline-block
        width: 18px
        height 12px
        background-size: 18px 12px
        background-repeat: no-repeat
        bg-image('bulletin')
      .bulletin-text
        vertical-align: top
        margin: 0 4px
        font-size: 10px
        text-overflow: ellipsis
      .icon-keyboard_arrow_right
        position: absolute
        color: #fff
        font-size: 10px
        top: 7px
        right: 12px
    .bg
      position: absolute
      top: 0
      left: 0
      width: 100%
      height: 100%
      filter: blur(10px)
      -webkit-filter: blur(10px)
      z-index: -1
      img
        width: 100%
        height: 100%;
    .details
      position: fixed
      top: 0
      left: 0
      width: 100%
      height: 100%
      backdrop-filter: blur(10px)
      overflow-y: scroll
      transition: all 0.5s
      background: rgba(7, 17, 27, 0.8)
      &.fade-enter-active
        opacity: 1
        background: rgba(7, 17, 27, 0.8)
      &.fade-enter, &.fade-leave-active
        opacity: 0
        background: rgba(7, 17, 27, 0)
      .details-wrapper
        width: 100%
        min-height: 100%
        margin-bottom: -64px
        .name
          font-size: 16px
          font-weight: 700
          color: rgb(255, 255, 255)
          line-height: 16px
          margin: 64px auto 16px auto
          text-align: center
        .details-main
          width: 80%
          margin: 0 auto
          .title
            display: flex
            align-items: center
            margin: 28px auto 24px auto
            .text
              font-size: 14px
              font-weight: 700
              color: rgb(255, 255, 255)
              margin: auto 12px
            .line
              flex: 1
              background-color: rgba(255, 255, 255, 0.2)
              width: 1px
              height: 1px
              align-items: center
        .supports
          margin: 24px auto 28px auto
          color: rgb(255, 255, 255)
          font-weight: 200
          font-size: 12px
          line-height: 12px
          & ul li
            padding: 0 0 12px 12px
            &:last-child
              padding-bottom: 0
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
        .bulletin
          margin-top: 24px
          & p
            font-size: 12px
            font-weight: 200
            color: rgb(255, 255, 255)
            line-height: 24px
      .details-close
        font-size: 32px
        color: rgba(255, 255, 255, 0.5)
        text-align: center

</style>
