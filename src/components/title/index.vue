<template>
  <div class="m-tit">
    <div class="m-tit__line"></div>
    <div class="m-tit__text">{{tit}}</div>
    <div class="m-tit__line"></div>
  </div>
</template>

<script type="text/javascript">
  export default{
    props: ['tit']
  }
</script>

<style lang="scss">
  .m-tit {
    display: flex;
    align-items: center;
    width: 80%;
    margin: 28px auto 24px;
    &__line {
      flex: 1;
      position: relative;
      height: 1px;
      background-color: rgba(255, 255, 255, .4);
    }
    &__text {
      font-weight: 700;
      padding: 0 12px;
      font-size: 14px;
    }
  }
</style>
