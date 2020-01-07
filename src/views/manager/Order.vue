<template>
  <div class="order">
    <van-nav-bar title="我的订单" />
    <van-tabs v-model="active" color="#1659a0">
      <van-tab title="全部">
      </van-tab>
      <van-tab title="未开始">
      </van-tab>
      <van-tab title="进行中">
      </van-tab> 
      <van-tab title="已完成">
      </van-tab>
    </van-tabs>
    <div>
      <ul>
        <briup-order-item 
        v-for="o in orders" 
        :key="o.id" 
        :data=o>  
        </briup-order-item>
      </ul>
    </div>
  </div>
</template>
<script>
import {  mapState } from 'vuex'
import {get} from '../../http/axios'
export default {
  data(){
    return {
      active:0,
      orders:[]
    }
  },
  computed:{
    ...mapState("user",["info"])
  },
  methods:{
    // 加载我的订单
    loadOrders(){
      let url="/order/query?customerId";
      let params={
        customerId:this.info.id
      }
      get(url,params).then((response)=>{
        this.orders=response.data;
      })
    },
  },
  created(){
    this.loadOrders();
  }
}
</script>
<style scoped>
.order {
  background: #f1f1f1;
}
</style>