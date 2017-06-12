<template>
  <div class="header">
    <div class="header__wrapper">
      <div class="header__avatar">
        <img height="64" width="64" :src="seller.avatar">
      </div>
      <div class="header__content">
        <div class="header__tit">
         <span class="header__brand">
         </span>
          <span class="header__name">{{seller.name}}</span>
        </div>
        <div class="header__desc">{{seller.description}}/{{seller.deliverytime}}分钟速送</div>
        <div v-if="seller.supports" class="header__support">
          <span class="header__support__icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="header__support__text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div v-if="seller.supports" class="header__sup cursor" @click.stop.prevent="showDetailModal">
        <span class="header__sup__count">{{ seller.supports.length }}个</span>
        <i class="iconfont icon-xiangyou1"></i>
      </div>
    </div>
    <div class="header__bulletin">
      <div class="header__bulletin__tit"></div>
      <div class="header__bulletin__text">{{seller.bulletin}}</div>
      <i class="iconfont icon-xiangyou1 cursor" @click.stop.prevent="showDetailModal"></i>
    </div>
    <div class="header__bgimg">
      <img :src="seller.avatar" width="100%" height="100%">
    </div>
    <!--模态框-->
    <transition
      appear
      name="csq"
      enter-active-class="animated bounceInDown"
      leave-active-class="animated bounceOutUp"
    >
      <div v-if="detailModalShow" class="header__detail">
        <div class="header__detail__wrapper">
          <div class="header__detail__main">
            <h2 class="header__detail__name">{{seller.name}}</h2>
            <div class="header__detail__star">
              <!--星星组件-->
              <star :size="48" :score="seller.score"></star>
            </div>
            <!--标题组件-->
            <tit tit="优惠信息"></tit>
            <ul v-if="seller.supports" class="header__detail__supports">
              <li class="supports__item" v-for="(item , index) in seller.supports">
                <span class="icon" :class="classMap[seller.supports[index].type]"></span>
                <span class="txt">{{seller.supports[index].description}}</span>
              </li>
            </ul>
            <!--标题组件-->
            <tit tit="商家公告"></tit>
          </div>
        </div>
        <div class="header__detail-close">
          <i class="iconfont icon-guanbi1 cursor" @click.stop.prevent="showDetailModal"></i>
        </div>
      </div>
    </transition>

  </div>
</template>

<script>

  import star from '../star/index'
  import tit from '../title/index'

  export default {
    props: {
      seller: {
        type: Object
      }
    },
    data() {
      return {
        detailModalShow: true
      }
    },
    methods: {
      showDetailModal () {
        this.detailModalShow = !this.detailModalShow
      }
    },
    created() {
      this.classMap = ['special', 'discount', 'special', 'invoice', 'guarantee']
    },
    components: {
      star,
      tit
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">

  @import '../../common/sass/index';

  .header {
    position: relative;
    color: #fff;
    font-size: 0;
    overflow: hidden;
    background-color: rgba(7, 17, 27, .5);
    &__wrapper {
      padding: 24px 12px 18px 24px;
      font-size: 0;
      display: flex;
      flex-flow: row nowrap;
      align-items: flex-start;
      position: relative;
    }
    &__avatar {
      > img {
        border-radius: 2px;
      }
    }
    &__content {
      font-size: 14px;
      margin-left: 16px;
    }
    &__tit {
      margin: 2px 0 8px 0;
      line-height: 18px;
      display: flex;
      flex-flow: row nowrap;
      overflow: hidden;
    }
    &__brand {
      height: 18px;
      width: 30px;
      background-color: #fff;
      @include bg-image('brand');
      background-size: 30px 18px;
      background-repeat: no-repeat;
    }
    &__name {
      font-size: 16px;
      margin-left: 6px;
      font-weight: 600;
    }
    &__desc {
      font-size: 12px;
      margin-bottom: 10px;
      line-height: 12px;
    }
    &__support {
      display: inline-flex;
      flex-flow: row nowrap;
      align-items: flex-end;
      justify-content: flex-start;
      &__icon {
        height: 12px;
        width: 12px;
        background-size: 12px 12px;
        background-repeat: no-repeat;
        &.decrease {
          @include bg-image('decrease_1');
        }
        &.discount {
          @include bg-image('discount_1');
        }
        &.guarantee {
          @include bg-image('guarantee_1');
        }
        &.invoice {
          @include bg-image('invoice_1');
        }
        &.special {
          @include bg-image('special_1');
        }
      }
      &__text {
        margin-left: 4px;
        font-size: 10px;
      }
    }
    &__sup {
      position: absolute;
      right: 12px;
      bottom: 18px;
      line-height: 24px;
      height: 24px;
      padding: 0 8px;
      font-size: 12px;
      border-radius: 14px;
      background-color: rgba(0, 0, 0, .2);
      text-align: center;
      .iconfont {
        font-size: 10px;
      }
    }
    &__bulletin {
      position: relative;
      height: 28px;
      line-height: 28px;
      padding: 0 22px 0 12px;
      overflow: hidden;
      background-color: rgba(0, 0, 0, .3);
      &__tit {
        display: inline-block;
        vertical-align: top;
        margin-top: 7px;
        padding: 6px 12px;
        @include bg-image('bulletin');
        background-size: 22px 12px;
        background-repeat: no-repeat;
      }
      &__text {
        display: inline-block;
        vertical-align: middle;
        white-space: nowrap;
        width: 90%;
        overflow: hidden;
        text-overflow: ellipsis;
        font-size: 10px;
        margin: 0 4px;
      }
      .iconfont {
        position: absolute;
        right: 10px;
        top: 1px;
        font-size: 8px;
      }
    }
    &__bgimg {
      position: absolute;
      left: 0;
      top: 0;
      width: 100%;
      height: 100%;
      z-index: -1;
      @include blur(10);
    }
    &__detail {
      position: fixed;
      width: 100%;
      height: 100%;
      top: 0;
      left: 0;
      overflow: auto;
      z-index: 999;
      background-color: rgba(0, 0, 0, .6);
      &__wrapper {
        min-height: 100%;
        width: 100%;
        @include clearfix;
      }
      &__main {
        margin-top: 64px;
        font-size: 12px;
        padding-bottom: 64px;
      }
      &-close {
        position: relative;
        width: 32px;
        height: 32px;
        margin: -64px auto 0 auto;
        font-size: 32px;
        @include clearfix;
      }
      &__name {
        line-height: 16px;
        text-align: center;
        font-size: 16px;
        font-weight: 700;
      }
      &__star {
        margin-top: 18px;
        padding: 2px 0;
        text-align: center;
      }

      &__supports {
        width: 80%;
        margin: 0 auto;
        .supports__item {
          margin-bottom: 12px;
          font-size: 0;
          &:last-child {
            margin-bottom: 0;
          }
          .icon {
            display: inline-block;
            height: 16px;
            width: 16px;
            vertical-align: middle;
            margin-right: 6px;
            background-size: 16px 16px;
            background-repeat: no-repeat;
            &.decrease {
              @include bg-image('decrease_2');
            }
            &.discount {
              @include bg-image('discount_2');
            }
            &.guarantee {
              @include bg-image('guarantee_2');
            }
            &.invoice {
              @include bg-image('invoice_2');
            }
            &.special {
              @include bg-image('special_2');
            }
          }
          .txt {
            font-size: 12px;
            vertical-align: middle;
          }
        }
      }
    }
  }
</style>

<style lang="scss">

</style>
