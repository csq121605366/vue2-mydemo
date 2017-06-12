<template>
  <div class="goods">
    <div class="menu__wrapper">
      <ul>
        <li v-for="(item , index) in goods" :key="index">
          <span v-show="item.type > 0" class="icon" :class="aMenuIcon[item.type]"></span>{{item.name}}
        </li>
      </ul>
    </div>
    <div class="foods__wrapper">
  
    </div>
  </div>
</template>

<script type="text/javascript">
import api from '../../service/getData.js'
import type from '../../store/type.js'
export default {
  props: {
    seller: {
      type: Object
    }
  },
  data() {
    return {
      goods: [],
      aMenuIcon: ['special', 'discount', 'special', 'invoice', 'guarantee']
    }
  },
  created() {
    api.getGoods().then(res => {
      if (res.data.errno === type.ERR_OK) {
        this.goods = res.data.data
        console.log(this.goods)
      }
    })
  }
}
</script>

<style lang="scss">
.goods {
  position: absolute;
  top: 174px;
  bottom: 46px;
  width: 100%;
  display: flex;
  overflow: hidden;
  .menu {
    &__wrapper {
      flex: 0 0 80px;
      width: 80px;
      background-color: #f3f5f7;
    }
  }
  .foods {
    &__wrapper {
      flex: auto;
    }
  }
}
</style>
