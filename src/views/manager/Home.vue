<template>
  <div class="home">
    <header class="header">
      <img src="../../assets/home.jpg" alt="">
    </header>
    <!-- 内容区域 -->
    <div>
      <!-- 分类6个 -->
      <!-- {{categories}} -->
      <van-grid :column-num="3" icon-size="70px">
        <van-grid-item v-for="value in categories" :key="value.id" :icon="value.icon" :text="value.name"/>
      </van-grid>

      <van-grid :column-num="2">
        <van-grid-item v-for="value in products" :key="value.id" :icon="value.icon" :text="value.name"/>
      </van-grid>
      
      

      <!-- 产品4个 -->
    </div>
   
  </div>
</template>
<script>

import { get,post } from '../../http/axios';
export default {
  data(){
    return{
    categories:[],
    products:[]
    }
  },
  created(){
    // 查询栏目信息
    this.loadCategories();
    // 查询产品
    this.loadProducts();

  },
  methods:{
    loadCategories(){
      let url="/category/findAll";
      get(url).then((response)=>{
        //  将数据中的前六个数组提取出来
        this.categories=response.data.slice(0,6);
      })
    },

    loadProducts(){
      let url="/product/query"
      let params={
          page:0,
          pageSize:10
      }
      post(url,params).then((response)=>{
          this.products=response.data.list;
      })
    }
  }
  
}
</script>
<style scoped>
.home {
  padding-bottom: 50px;
}
.header {
  height: 300px;
  overflow: hidden;
}
.header img {
  width: 100%;
}
</style>