<template>
  <div class="shelf-item-book">
    <img :src="data.cover" class="shelf-item-book-cover">
  </div>
</template>

<script>
export default {
 name: 'ShelfItemImage',
  props: {
   data: Object
  }
}
</script>

<style lang="scss" scoped>
@import "../../assets/styles/global";
.shelf-item-book {
  width: 100%;
  height: 100%;
  .shelf-item-book-cover {
    width: 100%;
    height: 100%;
  }
}
</style>
