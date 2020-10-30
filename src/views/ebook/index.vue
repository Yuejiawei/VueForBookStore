<template>
  <div class="ebook" ref="ebook">
    <ebook-header></ebook-header>
    <ebook-title></ebook-title>
    <ebook-reader></ebook-reader>
    <ebook-menu></ebook-menu>
    <ebook-bookmark></ebook-bookmark>
    <ebook-footer></ebook-footer>
  </div>
</template>

<script>
  import EbookTitle from '../../components/ebook/EbookTitle'
  import EbookReader from '../../components/ebook/EbookReader'
  import EbookMenu from '../../components/ebook/EbookMenu'
  import EbookBookmark from '../../components/ebook/EbookBookmark'
  import { getReadTime, saveReadTime } from '../../utils/localStorage'
  import { ebookMixin } from '../../utils/mixin'
  import EbookHeader from '../../components/ebook/EbookHeader'
  import EbookFooter from '../../components/ebook/EbookFooter'
  export default {
    name: 'index',
    mixins: [ebookMixin],
    components: {
      EbookTitle,
      EbookReader,
      EbookMenu,
      EbookBookmark,
      EbookHeader,
      EbookFooter
    },
    methods: {
      startLoopReadTime () {
        let readTime = getReadTime(this.fileName)
        if (!readTime) {
          readTime = 0
        }
        this.task = setInterval(() => {
          readTime++
          if (readTime % 30) {
            saveReadTime(this.fileName, readTime)
          }
        }, 1000)
      },
      move (v) {
        this.$refs.ebook.style.top = v + 'px'
      },
      restore () {
        this.$refs.ebook.style.top = 0
        this.$refs.ebook.style.transition = 'all .2s linear'
        setTimeout(() => {
          this.$refs.ebook.style.transition = ''
        }, 200)
      }
    },
    watch: {
      offsetY (v) {
        if (!this.menuVisible && this.bookAvailable) {
          if (v > 0) {
            this.move(v)
          } else if (v === 0) {
            this.restore()
          }
        }
      }
    },
    mounted () {
      this.startLoopReadTime()
    },
    beforeDestroy () {
      if (this.task) {
        clearInterval(this.task)
      }
    }
  }
</script>

<style lang="scss" scoped>
@import "../../assets/styles/global";
  .ebook {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
  }
</style>
