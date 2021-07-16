<template>
    <div class="tab-bar-item" @click="itemClick">
      <div v-if="isActive" ><slot name="item-icon"></slot></div>
      <div v-else><slot name="item-icon-active"></slot></div>
      <div :style="activeStyle"><slot name="item-text"></slot></div>
<!--      <img src="../../assets/img/tabbar/zhuye0.svg">-->
<!--      <div>首页</div>-->
       </div>
</template>

<script>
export default {
  name: "TabBarItem",
  props:{
    path:String,   //path 接收点击item的路径 指定为String类型
    activeColor:{
      type:String,
      default:'#de8bb0'
    }
  },
  data(){
    return{
      //isActive:false,
    }
  },
  computed:{
    isActive(){
      return this.$route.path.indexOf(this.path)      //! == -1就找到了就为true
    },
    activeStyle(){
      return this.isActive ? {}:{color: this.activeColor}
    }
  },
  methods:{
    itemClick(){
      this.$router.replace(this.path).catch(err=>err)
      console.log(this.path)
    }
  }
}
</script>

<style scoped>
.tab-bar-item{
  flex:1;
  text-align: center;
  height: 49px;
  font-size: 14px;
}
.tab-bar-item img{
  width: 24px;
  height: 24px;
  margin-top: 3px;
  vertical-align: middle;/*去掉图片底下默认3像素*/
  margin-bottom: 2px;
}
.active{
  color: #de8bb0;
}
</style>
