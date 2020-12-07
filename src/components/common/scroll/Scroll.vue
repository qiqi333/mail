<template>
  <!--ref/children父子组件访问-->
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
  import BScroll from 'better-scroll'

  export default {
    name: "Scroll",
    props: {
      probeType: {
        type: Number,
        default: 0
      },
      pullUpLoad: {
        type: Boolean,
        default: false
      }
    },
    data() {
      return {
        scroll: null,
        message: '哈哈哈'
      }
    },
    mounted() {
      // 1.创建BScroll对象
      //this.scroll = new BScroll(document.querySelect('.content'),{
      //document.querySelect('.content')在有多个content时，获取的是第一个最外层的content对象，这里使用不合适
      this.scroll = new BScroll(this.$refs.wrapper, {
        click: true,
        //有的地方不需要实时监听位置，probeType直接设为3会影响性能，根据传入的值决定
        probeType: this.probeType,
        pullUpLoad: this.pullUpLoad
      })
      this.scroll.scrollTo(0, 0)

      // 2.监听滚动的位置
      if (this.pullUpLoad === 2 || this.pullUpLoad === 3){
        this.scroll.on('scroll', (position) => {
          // console.log(position);
          this.$emit('scroll', position)
        })
      }

      // console.log(this.scroll);
      // 3.监听上拉事件
      if (this.pullUpLoad){
        this.scroll.on('pullingUp', () => {
          //console.log('上拉加载更多');
          this.$emit('pullingUp')
        })
      }
    },
    methods: {
      scrollTo(x, y, time=300) {
        this.scroll && this.scroll.scrollTo(x, y, time)
      },
      refresh() {
        this.scroll && this.scroll.refresh()
      },
      finishPullUp() {
        this.scroll && this.scroll.finishPullUp()
      }
    },
    //处理可滚动区域问题-方法一
    //方法二:https://www.bilibili.com/video/BV15741177Eh?p=173
    updated() {
      //重新计算高度
     // console.log('重新计算高度');
      this.scroll && this.scroll.refresh();
    //  this.scroll.finishPullUp();
    }
  }
</script>

<style scoped>

</style>
