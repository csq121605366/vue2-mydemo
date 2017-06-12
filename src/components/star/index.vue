<template>
  <div class="star" :class="starType">
    <span v-for="(itemClass , index) in itemClasses" :class="itemClass" :key="index" class="star-item"></span>
  </div>
</template>

<script type="text/javascript">
  import type from '../../store/type'

  export default{
    props: {
      size: {
        type: Number
      },
      score: {
        type: Number
      }
    },
    computed: {
      starType () {
        return 'star-' + this.size
      },
      itemClasses () {
        // 如果不存在则返回false
        if (this.score === 'undefined') return false
        let result = []
        // 该算法主要是先乘以2取整然后除以2
        let score = Math.floor(this.score * 2) / 2
        let hasDecimal = score % 1 !== 0
        let integer = Math.floor(score)
        for (let i = 0; i < integer; i++) {
          result.push(type.STAR_ON)
        }
        if (hasDecimal) {
          result.push(type.STAR_HALF)
        }
        while (result.length < type.STAR) {
          result.push(type.STAR_OFF)
        }
        return result
      }
    }
  }
</script>

<style lang="scss">
  @import "../../common/sass/index";

  .star {
    font-size: 0;
    &-item {
      display: inline-block;
      background-repeat: no-repeat;
    }
    &.star-48 {
      .star-item {
        height: 20px;
        width: 20px;
        margin-right: 22px;
        background-size: 20px 20px;
        &:last-child {
          margin-right: 0;
        }
        &.on {
          @include bg-image('star48_on');
        }
        &.half {
          @include bg-image('star48_half');
        }
        &.off {
          @include bg-image('star48_off');
        }
      }
    }
    &.star-36 {
      .star-item {
        height: 15px;
        width: 15px;
        margin-right: 6px;
        background-size: 15px 15px;
        &:last-child {
          margin-right: 0;
        }
        &.on {
          @include bg-image('star36_on');
        }
        &.half {
          @include bg-image('star36_half');
        }
        &.off {
          @include bg-image('star36_off');
        }
      }
    }
    &.star-24 {
      .star-item {
        height: 10px;
        width: 10px;
        margin-right: 3px;
        background-size: 10px 10px;
        &:last-child {
          margin-right: 0;
        }
        &.on {
          @include bg-image('star24_on');
        }
        &.half {
          @include bg-image('star24_half');
        }
        &.off {
          @include bg-image('star24_off');
        }
      }
    }

  }
</style>
