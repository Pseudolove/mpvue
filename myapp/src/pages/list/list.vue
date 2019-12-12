<template>
  <div class="wrap">
    <div>我的当当</div>
    <!-- <div class="box" @click="click(1)">点我</div> -->
    <!-- <div class="item" v-for="(item,index) in list" wx:key="index">
        <img :src="item.image" class="img">
        <div>{{item.name}}</div>
        <div>{{item.desc}}</div>
        <div>￥{{item.price}}</div>
    </div> -->
  </div>
</template>
<script>
// export default {
//   data() {
//     return {
//       list: []
//     };
//   },

//   methods: {
//     // click(e) {
//     //   console.log(e);
//     // }
//   },
//   mounted() {
//       wx.request({
//           url:"http://127.0.0.1:8080/data.json",
//           success:(res)=>{
//               this.list = res.data;
//               console.log(res)
//           }
//       })
//   },
//   created() {}
// };
</script>
<style scoped>
/* .box {
  width: 100px;
  height: 100px;
  background-color: #ff0;
} */
/* .wrap {
  display: flex;
  flex-wrap: wrap
}
.item {
  width: 375rpx;
  height: 600rpx;
}
.img {
  width: 375rpx;
  height: 450rpx;
} */
</style>