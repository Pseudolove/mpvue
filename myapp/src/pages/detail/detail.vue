<template>
  <div class="wrap">
    <div class="top"></div>
    <div class="img">
      <img :src="newbook.image" class="bookimg" />
    </div>
    <div class="top"></div>
    <div class="name">
      <p class="dang">当当自营</p>
      <text>{{newbook.name}}</text>
    </div>
    <div class="jie">{{newbook.desc}}</div>
    <div class="price">
      <p class="newprice">
        ￥
        <text class="np">{{newbook.price}}</text>
        <text class="zhe">（1.1折）</text>
      </p>
      <p class="rmb">
        <img src="/static/images/rmb.png" class="ren" />
        <text class="jia">降价通知</text>
      </p>
    </div>
    <div class="oldprice">原价：￥{{newbook.old_price}}</div>
    <div class="buy">
      <div class="dian">
        <img src="/static/images/dian.png" class="pu" />
        <p class="text">店铺</p>
      </div>
      <div class="cart" @click="cart">
        <img src="/static/images/buy.png" class="pu" />
        <p class="text">购物车</p>
      </div>
    </div>
    <div class="li">
      <div class="yel">立即购买</div>
      <div class="red" @click="addCart(newbook.id)" >加入购物车</div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      books: [],
      newbook: {}
    };
  },

  methods: {
    addCart(id) {
      let products = wx.getStorageSync("cart") || [];
      let index = products.findIndex(item => {
        return item.id == id;
      });
      if (index != -1) {
        products[index].count += 1;
      } else {
        this.newbook.count = 1;
        this.newbook.checked = true;
        products.push(this.newbook);
      }
      wx.setStorageSync("cart", products);
      wx.showToast({
        title: '加入购物车成功',
        icon: 'success',
        duration: 1000,
        success: (res)=>{
          wx.setStorageSync("cart",products)
        },
      });
    },
    cart(){
      wx.switchTab({url:'/pages/logs/main'});
    }
  },
  onLoad(e) {
    let id = e.id;
    let book = this.books.find(item => {
      return item.id == id;
    });
    this.newbook = book;
    console.log(book);
  },
  created() {
    wx.request({
      url: "http://127.0.0.1:8080/book.json",
      success: res => {
        console.log(res);
        this.books = res.data;
      }
    });
  }
};
</script>
<style scoped>
.top {
  width: 750rpx;
  height: 5rpx;
  background-color: #ddd;
  margin-bottom: 10px;
}
.img {
  width: 750rpx;
  height: 500rpx;
  text-align: center;
  margin-bottom: 10px;
}
.bookimg {
  width: 450rpx;
  height: 500rpx;
}
.name {
  display: flex;
  margin-left: 20px;
  margin-top: 20px;
}
.dang {
  width: 70px;
  height: 20px;
  text-align: center;
  line-height: 20px;
  background-color: #f00;
  color: #fff;
  margin-right: 20rpx;
  border-radius: 10px;
}
.jie {
  margin-top: 20rpx;
  box-sizing: border-box;
  padding: 0 20px;
  font-size: 14px;
  color: #999;
}
.price {
  width: 750rpx;
  height: 30px;
  display: flex;
  margin-top: 20px;
}
.newprice {
  color: #f00;
  box-sizing: border-box;
  padding: 0 20px;
  margin-right: 20px;
}
.np {
  font-size: 22px;
  font-weight: bold;
}
.zhe {
  font-size: 14px;
  color: #999;
}
.rmb {
  width: 200rpx;
  height: 20px;
  border: 1px solid #000;
  border-radius: 10px;
  text-align: center;
  line-height: 20px;
}
.ren {
  width: 50rpx;
  height: 50rpx;
}
.jia {
  position: relative;
  top: -8px;
}
.oldprice {
  box-sizing: border-box;
  padding: 0 20px;
  color: #999;
}
.buy {
  width: 250rpx;
  position: fixed;
  bottom: 0;
  left: 0;
  display: flex;
  justify-content: space-between;
  box-sizing: border-box;
  padding: 0 0 0 20px;
}
.pu {
  width: 60rpx;
  height: 60rpx;
}
.li {
  width: 500rpx;
  height: 100rpx;
  display: flex;
  position: fixed;
  bottom: 0;
  left: 150px;
  color: #fff;
  font-size: 18px;
}
.yel {
  width: 225rpx;
  background-color: #ff0;
  text-align: center;
  line-height: 50px;
}
.red {
  width: 225rpx;
  background-color: #f00;
  text-align: center;
  line-height: 50px;
}
</style>