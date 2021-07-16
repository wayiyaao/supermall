<template>
<div>
  <div class="wrapper" ref="aaa">
    <ul class="content">

      <li>lalal </li>
      <li>lalal </li>
      <li>lalal </li>
      <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li>
      <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li>
      <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li>
      <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li>
      <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li>
      <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li>
      <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li>
      <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li>
      <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li>
      <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li>
      <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li> <li>lalal </li>

    </ul>
  </div>
</div>
</template>

<script>
import BScroll from "better-scroll";
export default {
  name: "Category",
  data(){
    return{
      scroll:null
    }
  },
  mounted() {
    // this.scroll = new BScroll('this.$refs.aaa',{
    //
    // })
    this.scroll = new BScroll(document.querySelector('.wrapper'),{
    probeType:3,  //实时监听滚动数据
    pullUpLoad:true  //上拉加载更多
    })
    this.scroll.on('scroll',(position) =>{
      console.log(position);
    })
    this.scroll.on('pullingUp',() =>{
      console.log('上拉加载更多');
    })
  }
}
</script>

<style scoped>
.wrapper{
  height: 300px;
  background-color: #ff5777;
}
</style>
