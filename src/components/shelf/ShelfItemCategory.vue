<template>
  <div class="shelf-item-category">
    <div class="shelf-item-category-list">
      <div class="shelf-item-category-list-item" v-for="(item, index) in data.itemList" :key="index">
        <img class="shelf-item-category-img" :src="item.cover">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ShelfItemCategory',
  props: {
    data: Object
  }
}
</script>

<style lang="scss" scoped>
  @import "../../assets/styles/global";
  .shelf-item-category {
    width: 100%;
    height: 100%;
    overflow: hidden;
    .shelf-item-category-list {
      width: 100%;
      height: 100%;
      display: flex;
      flex-flow: row wrap;
      padding-top: px2rem(5);
      box-sizing: border-box;
      .shelf-item-category-list-item {
        flex: 0 0 33.3%;
        width: 33.33%;
        height: 33.33%;
        box-sizing: border-box;
        &:nth-child(3n+1) {
          padding: 0 px2rem(2.5) px2rem(5) px2rem(5);
        }
        &:nth-child(3n+2) {
          padding: 0 px2rem(2.5) px2rem(5) px2rem(2.5);
        }
        &:nth-child(3n+3) {
          padding: 0 px2rem(5) px2rem(5) px2rem(2.5);
        }
        .shelf-item-category-img {
          width: 100%;
          height: 100%;
        }
      }
    }
  }
</style>
