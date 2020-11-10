<template>
  <div class="shelf-search-wrapper">
    <div class="shelf-search">
      <div class="search-wrapper">
        <div class="icon-search-wrapper">
          <span class="icon-search icon"></span>
        </div>
        <div class="search-input-wrapper">
          <input type="text" class="search-input" :placeholder="$t('shelf.search')"
          @click="onSearchClick" v-model="searchText">
        </div>
        <div class="icon-clear-wrapper" v-show="searchText.length > 0" @click="clearSearchText">
          <span class="icon-close-circle-fill"></span>
        </div>
      </div>
      <div class="icon-locale-wrapper" v-if="!ifInputClicked" @click="switchLocale">
        <span class="icon-cn icon" v-if="lang === 'cn'"></span>
        <span class="icon-en icon" v-else></span>
      </div>
      <div class="cancel-btn-wrapper" @click="onCancelClick" v-else>
        <div class="cancel-text">{{$t('shelf.cancel')}}</div>
      </div>
    </div>
  </div>
</template>

<script>
import { setLocalStorage } from '@/utils/localStorage'

export default {
  name: 'ShelfSearch',
  data () {
    return {
      ifInputClicked: false,
      searchText: ''
    }
  },
  methods: {
    onSearchClick () {
      this.ifInputClicked = true
    },
    onCancelClick () {
      this.ifInputClicked = false
    },
    switchLocale () {
      if (this.lang === 'en') {
        this.$i18n.locale = 'cn'
      } else {
        this.$i18n.locale = 'en'
      }
      setLocalStorage('locale', this.$i18n.locale)
    },
    clearSearchText () {
      this.searchText = ''
    }
  },
  computed: {
    lang () {
      return this.$i18n.locale
    }
  }
}
</script>

<style lang="scss" scoped>
  @import "../../assets/styles/global";
  .shelf-search-wrapper {
    position: relative;
    z-index: 105;
    width: 100%;
    height: px2rem(94);
    font-size: px2rem(16);
    background: #fff;
    .shelf-search {
      position: absolute;
      top: px2rem(42);
      left: 0;
      width: 100%;
      height: px2rem(52);
      z-index: 105;
      display: flex;
      .search-wrapper {
        flex: 1;
        display: flex;
        margin: px2rem(8) 0 px2rem(8) px2rem(10);
        border-radius: px2rem(3);
        border: px2rem(1) solid #ccc;
        .icon-search-wrapper {
          flex: 0 0 px2rem(22);
          @include right;
          .icon-search {
            font-size: px2rem(12);
          }
        }
        .search-input-wrapper {
          flex: 1;
          padding: 0 px2rem(10);
          box-sizing: border-box;
          @include center;
          .search-input {
            width: 100%;
            font-size: px2rem(14);
            border: none;
            color: #333;
            &:focus {
              outline: none;
            }
            &::-webkit-input-placeholder {
              font-size: px2rem(14);
              color: #ccc;
            }
          }
        }
        .icon-clear-wrapper {
          flex: 0 0 px2rem(24);
          @include left;
          .icon-close-circle-fill {
            font-size: px2rem(14);
            color: #ccc;
          }
        }
      }
      .icon-locale-wrapper {
        flex: 0 0 px2rem(55);
        @include center;
        .icon-cn, .icon-en {
          font-size: px2rem(22);
          color: #666;
        }
      }
      .cancel-btn-wrapper {
        flex: 0 0 px2rem(55);
        @include center;
        .cancel-text {
          font-size: px2rem(14);
          color: $color-blue;
        }
      }
    }
  }
</style>
