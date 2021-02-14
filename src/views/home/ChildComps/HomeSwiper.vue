<template>
  <swiper>
    <swiper-item v-for="item in banners">
      <a :href="item.link">
        <img :src="item.image" alt="" @load="ImageLoad">
      </a>
    </swiper-item>
  </swiper>
</template>

<script>
import {Swiper, SwiperItem} from 'components/common/swiper'
export default {
  name: "HomeSwiper",
  props: {
    banners: {
      tpye: Array,
      default() {
        return []
      }
    }
  },
  data(){
    return {
      isLoad:false
    }
  },
  components: {
    Swiper,
    SwiperItem
  },
  methods: {
    ImageLoad() {
      if (!this.isLoad){
        this.$emit('HomeSwiper')
        this.isLoad = true
      }
    }
  }
}
</script>