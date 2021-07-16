<template>
<div id="home">
  <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
  <tab-control :titles="['流行','新款','精选']"
               @tabClick = "tabClick"
               class="tab-control"
               ref="tabControl1" v-show="isTabFixed"/>
  <scroller class="content"
            ref="scroller"
            :probe-type="3"
            @scroll="contentScroll"
            :pull-up-load="true"
            @pullingUp="loadMore">
    <home-swiper :banners="banners" @swiperImageLoad="swiperImageLoad"/>
    <home-recommend-view :recommends="recommends"></home-recommend-view>
    <home-feature-view></home-feature-view>
    <tab-control :titles="['流行','新款','精选']"
                 @tabClick = "tabClick"

                 ref="tabControl2"/>
    <goods-list :goods="showGoods"/>
  </scroller>
  <back-top @click.native="backClick" v-show="isShowBackTop"/>


</div>
</template>

<script>
import NavBar from "../../components/commom/navbar/NavBar";
import TabControl from "../../components/content/tabControl/TabControl";
import GoodsList from "../../components/content/goods/GoodsList";
import Scroller from "../../components/commom/scroller/Scroller";
import BackTop from "../../components/content/backTop/BackTop";


import HomeSwiper from "./childComps/HomeSwiper";
import HomeRecommendView from "./childComps/HomeRecommendView";
import HomeFeatureView from "./childComps/HomeFeatureView";


import {
  getHomeMultidata,
  getHomeGoods,
} from "../../network/home";

export default {
  name: "Home",
  components:{
    NavBar,
    TabControl,
    GoodsList,
    Scroller,
    BackTop,
    HomeSwiper,
    HomeRecommendView,
    HomeFeatureView,

  },
  data(){
    return{
      banners:[],
      recommends:[],
      goods:{
        'pop':{page:0,list:[]},
        'new':{page:0,list:[]},
        'sell':{page:0,list:[]},
      },
      currentType:'pop',
      isShowBackTop:false,
      tabOffsetTop: 0,
      isTabFixed:false
    }
  },
  created() {
    //请求多个数据
    this.getHomeMultidata()
    this.getHomeGoods('pop')
    this.getHomeGoods('new')
    this.getHomeGoods('sell')


  },
  mounted() {


  },
  computed:{
    showGoods(){
      return this.goods[this.currentType].list
    }
  },
  methods:{
    /*
    * 事件监听相关方法
    * */
    // //防抖
    // debounce(func,delay){
    //   let timer = null
    //   return function (){
    //     if(timer)clearTimeout(timer)
    //     timer = setTimeout(() => {
    //
    //     })
    //   }
    // },
    tabClick(index){
      // console.log(index)
      switch (index){
        case 0:
          this.currentType = 'pop'
          break
        case 1:
          this.currentType = 'new'
          break
        case 2:
          this.currentType = 'sell'
          break
      }
      this.$refs.tabControl1.currentIndex = index;
      this.$refs.tabControl2.currentIndex = index;
    },
    backClick(){
      this.$refs.scroller.scrollTo(0,0,500)
    },
    contentScroll(position){
      //1.判断BackTop是否显示
      this.isShowBackTop = -position.y > 1000
      //决定tabContent是否吸顶（position:fixed）
      this.isTabFixed = (-position.y) > this.tabOffsetTop
    },
    loadMore(){
      this.getHomeGoods(this.currentType)

      this.$refs.scroller.scroller.refresh()
    },
    swiperImageLoad(){
      //所有组件都有一个$el：用于获取组件中的元素
     this.tabOffsetTop = this.$refs.tabControl2.$el.offsetTop
    },
    /*
    * 网络请求相关方法
    * */
    getHomeMultidata(){
      getHomeMultidata().then(res =>{
        //console.log(res);
        this.banners = res.data.banner.list     //取出请求到的数据中的banner数据  并以数组形式输出方便后期取用
        this.recommends = res.data.recommend.list
      })
    },
    getHomeGoods(type){
      const page = this.goods[type].page + 1
      getHomeGoods(type,page).then(res =>{
        console.log(res)
        this.goods[type].list.push(...res.data.list)
        this.goods[type].page += 1

        this.$refs.scroller.finishPullUp()
      })
    }
  }
}
</script>

<style scoped>
#home{
  /*padding-top: 44px ;*/
  /*视口vh*/
  height: 100vh;
}
.home-nav{
  background-color: var(--color-tint);
  color: white;
  /*position: fixed;*/
  /*left: 0;*/
  /*top: 0;*/
  /*right: 0;*/
  /*z-index: 9;*/
}

.content{
  height: calc(100% - 93px);
  overflow: hidden;
  /*margin-top: 44px;*/
}
.tab-control{
  position: relative;
  z-index: 9;
}
/*.fixed{*/
/*  position: fixed;*/
/*  top: 44px;*/
/*  left: 0;*/
/*  right: 0;*/
/*}*/
</style>
