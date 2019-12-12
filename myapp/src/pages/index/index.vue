<template>
    <div class="wrap">
        <div class="top">
          <img src="/static/images/logo.png" class="img"></img>
          <div class="inp">
            <img src="/static/images/sousuo.png" class="img">
            <input type="text" placeholder="DK">
          </div>
          <img src="/static/images/right.png" class="img"></img>
        </div>
        <swiper indicator-dots="true" autoplay="true" class="banners" interval="2000" circular="true">
          <swiper-item class="banner">
            <img src="/static/images/banner1.jpg" class="imgs">
          </swiper-item>
          <swiper-item class="banner">
            <img src="/static/images/banner2.jpg" class="imgs">
          </swiper-item>
          <swiper-item class="banner">
            <img src="/static/images/banner3.jpg" class="imgs">
          </swiper-item>
          <swiper-item class="banner">
            <img src="/static/images/banner4.jpg" class="imgs">
          </swiper-item>
          <swiper-item class="banner">
            <img src="/static/images/banner5.jpg" class="imgs">
          </swiper-item>
        </swiper>
        <ul>
          <li v-for="(item,index) in list" :key="index">
            <img :src="item.image" class="li-img">
          </li>
        </ul>
        <div class="hui"></div>
        <div class="gao">
          <img src="/static/images/guanggao.png" class="gao-img">
        </div>
        <div class="book">
            <div class="book-one" @click="detail(item.id)" v-for="(item,index) in book" :key="index" wx:key="index">
                <img :src="item.image" class="book-img">
                <p class="name">{{item.name}}</p>
                <p class="desc">{{item.desc}}</p>
                <div class="dang">
                  <p class="bor">当当自营</p>
                  <p class="bgc">限时抢</p>
                </div>
                <p class="price">￥{{item.price}}</p>
            </div>
        </div>
    </div>
</template>
<script>
export default {
  data(){
    return{
      list:[],
      book:[]
    }
  },
   
  methods:{
    detail(id){
      console.log(id)
      const url = '/pages/detail/main?id='+id
      wx.navigateTo({ url,
      success:res=>{
        console.log(res)
      },
      fail:err=>{
        console.log(err)
      }
      })
    }
  },
  mounted() {
     wx.request({
          url:"http://127.0.0.1:8080/type.json",
          success:(res)=>{
              this.list = res.data;
              // console.log(res)
          }
      })
     wx.request({
          url:"http://127.0.0.1:8080/book.json",
          success:(res)=>{
              this.book = res.data;
              // console.log(res)
          }
      })
  },
  created(){
   
  }
}
</script>
<style scoped>
  .top {
    display: flex;
    justify-content: space-between;
    box-sizing: border-box;
    padding: 0 20rpx;
  }
  .img {
    width: 50rpx;
    height: 50rpx;
  }
  .inp {
    width: 550rpx;
    height: 50rpx;
    background-color: #eee;
    border-radius: 25rpx;
    line-height: 50rpx;
    display: flex;
    box-sizing: border-box;
    padding: 0 20rpx;
  }
  input {
    text-indent: 20rpx;
    width: 550rpx;
    height: 50rpx;
  }
  .banner {
    width: 750rpx;
    height: 500rpx;
  }
  .imgs {
    width: 100%;
    height: 100%;
  }
  .banners {
    margin-top: 20rpx;
  }
  ul {
    display: flex;
    flex-wrap: wrap
  }
  li {
    list-style: none;
  }
  .li-img {
    width: 150rpx;
    height: 150rpx;
  }
  .hui {
    width: 750rpx;
    height: 20rpx;
    background-color: #EFF4FA;
  }
  .gao {
    width: 750rpx;
    height: 240rpx;
    margin-top: 30rpx;
  }
  .gao-img {
    width: 100%;
    height: 100%;
  }
  .book {
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
    margin-top: 30rpx;
  }
  .book-one {
    width: 360rpx;
    height: 600rpx;
  }
  .book-img {
    width: 330rpx;
    height: 400rpx;
  }
  .dang {
    display: flex;
    margin-top: 10rpx;
  }
  .name {
    font-weight: bold;
  }
  .bor {
    color: #f00;
    border: 1px solid #f00;
    margin-right: 30rpx;
  }
  .bgc {
    width: 100rpx;
    text-align: center;
    color: #fff;
    background-color: #f00;
  }
  .price {
    font-size: 18px;
    font-weight: bold;
    color: #f00;
    text-align: left;
    margin-top: 10rpx;
  }
  .desc {
    font-size: 14px;
    color: #666;
    width: 330rpx;
    height: 50rpx;
    text-overflow: ellipsis;
    overflow: hidden;
    white-space: nowrap;
  }
</style>