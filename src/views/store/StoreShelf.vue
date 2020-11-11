<template>
<div class="store-shelf">
  <shelf-title></shelf-title>
  <scroll class="store-shelf-scroll-wrapper" :top="0" :bottom="scrollBottom" @onScroll="onScroll" ref="scroll">
    <shelf-search></shelf-search>
    <shelf-list></shelf-list>
  </scroll>
  <shell-footer></shell-footer>
</div>
</template>

<script>
import ShelfTitle from '@/components/shelf/ShelfTitle'
import { storeShelfMixin } from '@/utils/mixin'
import Scroll from '@/components/common/Scroll'
import { shelf } from '@/api/store'
import ShelfSearch from '@/components/shelf/ShelfSearch'
import ShelfList from '@/components/shelf/ShelfList'
import { appendAddToShelf } from '@/utils/store'
import ShellFooter from '@/components/shelf/ShellFooter'
export default {
  name: 'StoreShelf',
  data () {
    return {
      scrollBottom: 0
    }
  },
  components: {
    ShellFooter,
    ShelfList,
    ShelfSearch,
    ShelfTitle,
    Scroll
  },
  mixins: [storeShelfMixin],
  methods: {
    onScroll (offsetY) {
      this.setOffsetY(offsetY)
    },
    getShelfList () {
      shelf().then(response => {
        if (response.status === 200 && response.data && response.data.bookList) {
          this.setShelfList(appendAddToShelf(response.data.bookList))
        }
      })
    }
  },
  mounted () {
    this.getShelfList()
  },
  watch: {
    isEditMode (isEditMode) {
      this.scrollBottom = isEditMode ? 48 : 0
      this.$nextTick(() => {
        this.$refs.scroll.refresh()
      })
    }
  }
}
</script>

<style lang="scss" scoped>
  @import "../../assets/styles/global";
  .store-shelf {
    width: 100%;
    height: 100%;
    background: #fff;
    z-index: 100;
    .store-shelf-scroll-wrapper {
      position: absolute;
      top: 0;
      left: 0;
      z-index: 101;
    }
  }
</style>
