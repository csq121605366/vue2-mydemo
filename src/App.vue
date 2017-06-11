<template>
  <div>
    <v-header></v-header>
    <div class="tab">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <!--路由视图-->
    <router-view></router-view>
  </div>
</template>

<script>
  import header from './components/header/header.vue'

  export default {
    components: {
      'v-header': header
    }
  }
</script>

<style lang="scss">

  @import 'common/sass/index';
  .tab {
    display: flex;
    justify-content: center;
    align-items: stretch;
    line-height: 40px;
    height: 40px;
    width: 100%;
    @include border-1px(#999);
    &-item {
      flex: 1;
      text-align: center;
      & > a {
        display: block;
        &:hover {
          color: orange;
        }
        &.active {
          color: #000;
        }
      }

    }
  }
</style>
