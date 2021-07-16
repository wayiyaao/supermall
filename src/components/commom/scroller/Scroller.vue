<template>
  <div ref="wrapper">
    <div>
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from 'better-scroll'
import Pullup from '@better-scroll/pull-up'
BScroll.use(Pullup)
export default {
  name: "scroller",
  data() {
    return {
      scroller:{
        type:Object,
        default() {
          return {}
        }
      }
    }
  },
  //接收父组件来的值
  props:{
    probeType:{
      type:Number,
      default:0
    },
    pullUpLoad:{
      type:Boolean,
      default:false
    }
  },
  mounted() {
    //创建BScroll对象
    this.scroller = new BScroll(this.$refs.wrapper, {
      probeType:this.probeType,
      click:true,
      pullUpLoad:true,
      observeDOM:true,
      observeImage:true
    })
    //监听滚动位置
    this.scroller.on('scroll', (position) => {
      // console.log(position);
      this.$emit('scroll', position)
    })
    //监听上拉事件
    this.scroller.on('pullingUp',() =>{
      //console.log('上拉加载更多')
      this.$emit('pullingUp')
    })
  },
  methods:{
    scrollTo(x, y, time=300) {
      this.scroller.scrollTo(0, 0, time)
    },
    finishPullUp(){
      this.scroller.finishPullUp()
    }
  }
}
</script>

<style scoped>

</style>
