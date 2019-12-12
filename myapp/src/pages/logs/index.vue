<template>
  <div class="wrap">
    <div class="wares" v-for="(item,index) in products" :key="index">
      <div class="book">
        <input type="checkbox" checked @click="single(index)" :checked="item.checked"/>
        <div class="img">
            <img :src="item.image">
        </div>
        <div class="name">{{item.name}}
          <span @click="del(index)">X</span>
        </div>
        <div class="price">
          <text class="newprice">￥{{item.price}}</text>
          <div class="oldprice">￥{{item.old_price}}</div>
          <div class="btns">
            <div class="add" @click="reduce(index)">-</div>
            <text class="count">{{item.count}}</text>
            <div class="add" @click="add(index)">+</div>
          </div>
        </div>
      </div>
      <div class="bottoms">
        <div class="gou">加价购</div>
        <p class="p1">购买一件，即可享受换购优惠</p>
        <div class="xuan">去选择></div>
      </div>
    </div>
    <div class="jiesuan">
      <div class="duo">
        <input type="checkbox" :checked="isCheckAll"  @click="checkAll" class="inp" />全选
      </div>
      <div class="all">合计：￥{{total}}元</div>
      <div class="account">结算（{{math}}）</div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      products:[],
      total:0,
      math:0,
      isCheckAll:true
    };
  },

  methods: {
    add(index){
      this.products[index].count +=1;
      wx.setStorageSync("cart", this.products);
      this.getTotal();
    },
    reduce(index){
      this.products[index].count -=1;
      if(this.products[index].count<1){
        this.products[index].count =1;
      }
      wx.setStorageSync("cart", this.products);
      this.getTotal();
    },
    del(index){
      this.products.splice(index,1)
      wx.setStorageSync("cart",this.products)
      this.getTotal();
    },
    getTotal(){
      let products = wx.getStorageSync("cart")||[];
      let total = 0;
      let math = 0;
      products.forEach(item => {
        if(item.checked==true){
          total += item.price*item.count;
          math+=item.count;
        }
      })
      this.total = total;
      this.math = math;
    },
    single(index){
      this.products[index].checked = !this.products[index].checked;
      wx.setStorageSync("cart",this.products);
      this.isCheckAll=this.products.every(item=>{
        return item.checked == true
      })
      this.getTotal();
    },
    checkAll(){
      this.isCheckAll=!this.isCheckAll;
      this.products.forEach(item=>{
        item.checked = this.isCheckAll
      })
      wx.setStorageSync("cart",this.products)
      this.getTotal();
    }
  },
  onShow(){
    let products = wx.getStorageSync("cart");
    this.products = products;
    this.getTotal();
  },
  created() {
    this.getTotal();
  } 
};
</script>
<style scoped>
.wrap {
  width: 750rpx;
  height: 100%;
  background-color: #eee;
  box-sizing: border-box;
  padding: 25rpx 0;
  padding-bottom: 100rpx;
}
.wares {
  width: 700rpx;
  height: 300rpx;
  background-color: #fff;
  border-radius: 20rpx;
  box-sizing: border-box;
  padding: 10px 0;
  margin-bottom: 10px;
  margin-left: 25rpx;
}
input {
  position: relative;
  top: 120rpx;
  float: left;
  margin-right: 10px;
  margin-left: 10px;
}
.img {
  width: 160rpx;
  height: 180rpx;
  float: left;
  margin-right: 10px;
}
img {
  width: 100%;
  height: 100%;
}
.price {
  display: flex;
  margin-top: 100rpx;
}
.newprice {
  font-size: 18px;
  font-weight: bold;
  color: #f00;
}
.btns {
  width: 80px;
  height: 80px;
  display: flex;
  justify-content: space-between;
  margin-left: 20px;
}
.count {
  position: relative;
  top: 5px;
}
.add {
  width: 30px;
  height: 30px;
  background-color: #eee;
  text-align: center;
  line-height: 30px;
  border-radius: 50%;
  font-size: 20px;
  font-weight: bold;
}
.oldprice {
  text-decoration: line-through;
  font-size: 14px;
  color: #999;
  margin-left: 10px;
}
.bottoms {
  width: 700rpx;
  height: 30rpx;
  display: flex;
  position: relative;
  top: -36px;
  justify-content: space-between;
  box-sizing: border-box;
  padding: 0 20px;
}
.gou {
  width: 80rpx;
  height: 30rpx;
  border: 1px solid #f00;
  color: #f00;
  text-align: center;
  line-height: 30rpx;
  font-size: 12px
}
.p1 {
  font-size: 12px;
  color: #999;
}
.jiesuan {
  width: 750rpx;
  height: 100rpx;
  position: fixed;
  bottom: 0;
  display: flex;
  justify-content: space-between;
  background-color: #fff;
}
.inp {
  position: relative;
  top: 0;
}
.all {
  line-height: 100rpx;
}
.duo {
  line-height: 100rpx
}
.account {
  width: 200rpx;
  height: 80rpx;
  background-color: #f00;
  color: #fff;
  text-align: center;
  line-height: 80rpx;
  font-size: 16px;
  border-radius: 50rpx
}
.name {
  position: relative;
}
span {
  position: absolute;
  right: 20rpx;
  font-size: 18px;
  font-weight: bold
}
</style>