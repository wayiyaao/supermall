<template>
<div>
  <nav-bar>
    <div slot="left" class="back" @click="backClick">
      <img src="../../../assets/img/common/back.svg">
    </div>
    <div class="title" slot="center">
      <div v-for="(item,index) in titles"
           class="title-item"
           :class="{active:index === currentIndex}" @click="titleClick(index)">{{item}}</div>
    </div>
  </nav-bar>
</div>
</template>

<script>
import NavBar from "../../../components/commom/navbar/NavBar";
export default {
  name: "DetailNavBar",
  components:{
    NavBar
  },
  data(){
    return{
      titles:['商品','参数','评论','推荐'],
      currentIndex:0
    }
  },
  methods:{
    titleClick(index){
      this.currentIndex = index
    },
    backClick(){
      this.$router.back()
    }
  }
}
</script>

<style scoped>
.title{
  display: flex;
  font-size: 13px;
}
.title-item{
  flex: 1;

}
.back img{
  vertical-align: middle;
}
.active{
  color: var(--color-tint);
}
</style>
