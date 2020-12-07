<template>
  <div class="goods">
<!--    <div v-for="(index,item) in goods"  :key="index">
      <img :src="item.show.img" alt="">
    </div>-->
    <!--v-for="(item,index)里，第一个参数是具体的值，第二个才是序号-->
    <goods-list-item v-for="(item,index) in goods" :key="index" :goods-item="item"/>
 <!--      {{goods}}-->
  </div>
</template>

<script>
  import GoodsListItem from "./GoodsListItem";

    export default {
      name: "GoodList",
      props: {
        goods: {
          type: Array,
          default() {
            return []
          }
        }
      },
      components: {
        GoodsListItem
      }
    }
</script>

<style scoped>
  .goods{
    display: flex;
    /*根据子组件GoodListItem的宽度进行打包，需要先设子组件的宽度百分比*/
    flex-wrap: wrap;
    /*让两个goods的内容均分一行*/
    justify-content: space-around;

    padding: 2px;
  }
</style>
