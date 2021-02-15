<template>
  <div id="detail">
    <detail-nav-bar></detail-nav-bar>
    <detail-swiper :top-images="topImages"></detail-swiper>
    <detail-base-info :goods="goods"/>
    <detail-shop-info :shop="shop"/>
  </div>
</template>


<script>
import DetailNavBar from './childComps/DetailNavBar.vue'
import DetailSwiper from './childComps/DetailSwiper.vue'
import DetailBaseInfo from './childComps/DetailBaseInfo'
import DetailShopInfo from './childComps/DetailShopInfo.vue'


import {getDetail, Goods, Shop} from 'network/detail'

export default {
  name: 'Detail',
  data() {
    return {
      iid: null,
      res: null,
      topImages: [],
      goods: {},
      shop: {}
    }
  },
  
  components: {
    DetailNavBar,
    DetailSwiper,
    DetailBaseInfo,
    DetailShopInfo,
  },

  created() {
    //1.保存iid
    this.iid = this.$route.params.id
    //2.根据iid获取详情页
    getDetail(this.iid).then(res => {
      console.log(res)
      //获取顶部轮播图片
      const data = res.result
      this.topImages = data.itemInfo.topImages
      //获取商品信息
      this.goods = new Goods(data.itemInfo, data.columns, data.shopInfo.services)
      //获取商家信息
      this.shop = new Shop(data.shopInfo)
    })
  }
}
</script>