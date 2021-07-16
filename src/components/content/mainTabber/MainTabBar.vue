<template>
  <tab-bar>
    <tab-bar-item path="/home">
      <img slot="item-icon" src="../../../assets/img/tabbar/zhuye0.svg">
      <img slot="item-icon-active" src="../../../assets/img/tabbar/zhuye1.svg">
      <div slot="item-text">首页</div>
    </tab-bar-item>
    <tab-bar-item path="/category">
      <img slot="item-icon" src="../../../assets/img/tabbar/fenlei0.svg">
      <img slot="item-icon-active" src="../../../assets/img/tabbar/fenlei1.svg">
      <div slot="item-text">分类</div>
    </tab-bar-item>
    <tab-bar-item path="/cart">
      <img slot="item-icon" src="../../../assets/img/tabbar/gouwuche0.svg">
      <img slot="item-icon-active" src="../../../assets/img/tabbar/gouwuche1.svg">
      <div slot="item-text">购物车</div>
    </tab-bar-item>
    <tab-bar-item path="/profile">
      <img slot="item-icon" src="../../../assets/img/tabbar/wode0.svg">
      <img slot="item-icon-active" src="../../../assets/img/tabbar/wode1.svg">
      <div slot="item-text">我的</div>
    </tab-bar-item>
  </tab-bar>
</template>

<script>
import TabBar from "../../commom/tabbar/TabBar";
import TabBarItem from "../../commom/tabbar/TabBarItem";
export default {
  name: "MainTabBar",
  components:{
    TabBar,
    TabBarItem
  }
}
</script>

<style scoped>

</style>
