<template>
  <swiper class="swiper-s">
    <swiper-item v-for="item in topImages">
      <img :src="item">
    </swiper-item>
  </swiper>
</template>

<script>
import {Swiper,SwiperItem} from "../../../components/commom/swiper";
export default {
  name: "DetailSwiper",
  props:{
    topImages:{
      type:Array,
      default(){
        return []
      }
    }
  },
  components:{
    SwiperItem,
    Swiper
  }
}
</script>

<style scoped>
.swiper-s{
  height: 400px;
  overflow: hidden;
}
</style>
