<template>
<div>
  <Upbar></Upbar>

<!--历史订单-->
  <div class="historyOrderCard" v-for="order in orders" :key="order.orderID"  @click="selectOrder(order.orderID)">
    <!--如果订单是没完成的，显示取餐码-->
    <div v-if="order.status <3">

    <van-cell icon="shop-o" :value="step[order.status]" is-link   size="large" title-style="font-size: 23px;"  value-class="step">
      <!-- 使用 title 插槽来自定义标题 -->
      <template #title>
        <span class="custom-title">{{order.orderID}}</span>
        <van-tag type="danger">取餐码</van-tag>
      </template>
    </van-cell>

    <van-cell center value-class="totalAmount" >
      <template #title>
          <van-image v-for="item in order.orderDetailList" :key="item.id" :src="item.dishPhoto" height="60px" fit="cover" style="margin-right: 10px;margin-top: 10px;margin-bottom: 10px"/>
    </template>
          <span class="custom-price" style="margin-right: 10px">¥{{order.totalAmount}}</span>
    </van-cell>
    </div>
    <!--如果订单是已完成的，显示下单时间-->
    <div v-else>
      <van-cell icon="shop-o" :value="step[order.status]" is-link   size="large"  value-class="step">
        <!-- 使用 title 插槽来自定义标题 -->
        <template #title>
          <span class="custom-title">{{order.createdTime}}</span>
<!--          <van-tag type="danger">取餐码</van-tag>-->
        </template>
      </van-cell>

      <van-cell center value-class="totalAmount" >
        <template #title>
          <van-image v-for="item in order.orderDetailList" :key="item.id" :src="item.dishPhoto" height="60px" fit="cover" style="margin-right: 10px;margin-top: 10px;margin-bottom: 10px"/>
        </template>
        <span class="custom-price" style="margin-right: 10px">¥{{order.totalAmount}}</span>
      </van-cell>
    </div>
  </div>

  <MenuFooter></MenuFooter>
</div>
</template>

<script>
import Upbar from "@/components/Upbar.vue";
import MenuFooter from "@/components/MenuFooter.vue";
export default {
  name: "OrderHistory",
  components: {
    MenuFooter,
    Upbar
  },
  data() {
    return {
      step: [
        "确认中",
        "配餐中",
        "待取餐",
        "已完成"
      ],
      orders: [
        {
          orderID: 12,
          createdTime: '2022年3月10日 11:30',
          status: 0,
          totalAmount: 20,
          orderDetailList: [
            {
              dishName: '番茄炒蛋',
              dishPhoto: 'http://rr707y5yy.hd-bkt.clouddn.com/%E6%B1%89%E5%A0%A1/%E5%8F%8C%E5%B1%82%E9%A6%99%E9%85%A5%E8%84%86%E9%B8%A1%E5%A0%A1.png'
            },
            {
              dishName: '麻婆豆腐',
              dishPhoto: 'http://rr707y5yy.hd-bkt.clouddn.com/%E6%B1%89%E5%A0%A1/%E5%8F%8C%E5%B1%82%E9%A6%99%E9%85%A5%E8%84%86%E9%B8%A1%E5%A0%A1.png'
            },
            {
              id: '3',
              name: '红烧肉',
              dishPhoto: 'http://rr707y5yy.hd-bkt.clouddn.com/%E6%B1%89%E5%A0%A1/%E5%8F%8C%E5%B1%82%E9%A6%99%E9%85%A5%E8%84%86%E9%B8%A1%E5%A0%A1.png'
            }
          ]
        },
        {
          orderID: 2,
          createdTime: '2022年3月9日 18:30',
          totalAmount: 20,
          status: 2,
          orderDetailList: [
            {
              dishName: '番茄炒蛋',
              dishPhoto: 'http://rr707y5yy.hd-bkt.clouddn.com/%E6%B1%89%E5%A0%A1/%E5%8F%8C%E5%B1%82%E9%A6%99%E9%85%A5%E8%84%86%E9%B8%A1%E5%A0%A1.png'
            },
            {
              dishName: '麻婆豆腐',
              dishPhoto: 'http://rr707y5yy.hd-bkt.clouddn.com/%E6%B1%89%E5%A0%A1/%E5%8F%8C%E5%B1%82%E9%A6%99%E9%85%A5%E8%84%86%E9%B8%A1%E5%A0%A1.png'
            },
          ]
        },
        {
          orderID: 3,
          createdTime: '2022年3月9日 18:30',
          totalAmount: 20,
          status: 3,
          orderDetailList: [
            {
              dishName: '番茄炒蛋',
              dishPhoto: 'http://rr707y5yy.hd-bkt.clouddn.com/%E6%B1%89%E5%A0%A1/%E5%8F%8C%E5%B1%82%E9%A6%99%E9%85%A5%E8%84%86%E9%B8%A1%E5%A0%A1.png'
            },
            {
              dishName: '麻婆豆腐',
              dishPhoto: 'http://rr707y5yy.hd-bkt.clouddn.com/%E6%B1%89%E5%A0%A1/%E5%8F%8C%E5%B1%82%E9%A6%99%E9%85%A5%E8%84%86%E9%B8%A1%E5%A0%A1.png'
            },
          ]
        }
      ]
    }
  },
  methods:{

    //点击跳转到订单详情页面
    selectOrder(orderID){
      this.$router.push({path:'/user/order',query:{orderID:orderID}})
    },

    //加载历史订单
    loadOrderHistory() {

      // this.orderNumber=res.data.createdTime.substring(3,10).replace(/-/g,"")+orderIdStr
      // this.$api.get('/orderinfo/orderhistory/'+sessionStorage.getItem('customerID')).then(res => {
      //   console.log(res.data);
      //
      // })
    }
  },
  mounted() {
    this.loadOrderHistory()
  }
}
</script>

<style scoped>
/*历史订单栏*/
.custom-title {
  margin-right: 4px;
  vertical-align: middle;
}
/*订单图片那部分设置宽一点,右边的部分少一点*/
.van-cell__value {
  max-width: 20%;
}

/*请取餐样式*/
.step{
  color: #000000;
}

/*价格样式*/
.totalAmount{
  color: rgba(0, 0, 0, 0.98);
  font-size: 15px;
}

/*每个历史订单card的样式*/
.historyOrderCard{
  border-radius: 10px;
  background-color: #ffffff;
  margin: 16px 16px 0 16px;
}

.van-cell{
  /*background-color: #f7e6e6;*/
  //border-radius: 10px;

}


/*加deep 改 vant样式*/
/deep/.van-cell--large{
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
  box-shadow: 5px 0px 10px rgba(0,0,0,0.1);
}
/deep/.van-cell--center{
  border-bottom-left-radius: 10px;
  border-bottom-right-radius: 10px;
/*再card下边加个阴影*/
  box-shadow: 0 10px 10px rgba(0,0,0,0.1);
}



.van-cell__title{
  text-align: left !important;
}
.search-icon {
  font-size: 16px;
  line-height: inherit;
}

</style>