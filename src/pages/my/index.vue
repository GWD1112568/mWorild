<template xlang="wxml" minapp="mpvue">
  <div class="root-wrap margin">
    <section class="userpic">
      <div class="user-left" @click="choosePicture">
        <img class="userpic-img" v-if="userInfo.userPic" :src="userInfo.userPic" />
        <img class="userpic-img" v-else src="/static/images/user.jpg" />
      </div>
      <div class="user-right">
        <div class="user-name">
          <card :text="userInfo.userName"></card>
        </div>
        <div class="user-phone">
          <card :text="userInfo.userPhone"></card>
        </div>
      </div>
      <a href="/" class="appointment">预约</a>
    </section>

    <section class="vipCard-box" style="background: url('/static/images/vipcardbg.png') no-repeat;background-size: 100% auto;">
      <div class="vipCard-top">
        <a href="/" class="go-recharge">充值</a>
        <p class="vipCard-txt">我的会员卡</p>
      </div>
      <div class="vipCard-bottom">
        <ul>
          <li>
            <i>¥{{vipCardInfo.balance}}</i>
            <p>余额</p>
          </li>
          <li class="li-center">
            <i>{{vipCardInfo.coupon}}</i>
            <p>卡卷</p>
          </li>
          <li>
            <i>¥{{vipCardInfo.coupons}}</i>
            <p>优惠卷</p>
          </li>
        </ul>
      </div>
    </section>

    <section class="user-process">
      <ul>
        <li>
          <a href="/">
            <p class="unpaid">
              <img src="/static/images/icon1.png" />
              <i v-if="userProcess.unpaid">{{userProcess.unpaid}}</i>
            </p>
            <span>未支付</span>
          </a>
        </li>
        <li>
          <a href="/">
            <p class="appointments">
              <img src="/static/images/icon2.png" />
              <i v-if="userProcess.appointments">{{userProcess.appointments}}</i>
            </p>
            <span>预约中</span>
          </a>
        </li>
        <li>
          <a href="/">
            <p class="consumed">
              <img src="/static/images/icon3.png" />
              <i v-if="userProcess.consumed">{{userProcess.consumed}}</i>
            </p>
            <span>已消费</span>
          </a>
        </li>
        <li>
          <a href="/">
            <p class="aftersales">
              <img src="/static/images/icon4.png" />
              <i v-if="userProcess.aftersales">{{userProcess.aftersales}}</i>
            </p>
            <span>售后</span>
          </a>
        </li>
      </ul>
    </section>

    <section class="user-process">
      <ul class="ulpro">
        <li>
          <a href="/">
            <p class="unpaid">
              <img src="/static/images/icon5.png" />
              <i v-if="userProcess.unpaid">{{userProcess.unpaid}}</i>
            </p>
            <span>我的核销</span>
          </a>
        </li>
        <li>
          <a href="/">
            <p class="appointments">
              <img src="/static/images/icon6.png" />
              <i v-if="userProcess.appointments">{{userProcess.appointments}}</i>
            </p>
            <span>我的预约</span>
          </a>
        </li>
      </ul>
    </section>
  </div>
</template>

<script>
  import Vue from 'vue'
  import card from '@/components/card'

  export default {
    data () {
      return {
        userInfo: {
          userName: 'windirs',
          userPhone: '18033441984',
          userPic: '/static/images/head.jpg'
        },
        vipCardInfo: {
          balance: 40,
          coupon: 6,
          coupons: 6
        },
        userProcess: {
          unpaid: 0,
          appointments: 0,
          consumed: 2,
          aftersales: 0
        }
      }
    },
    methods: {
      choosePicture () {
        let vuer = this
        wx.chooseImage({
          count: 1,
          sizeType: ['original', 'compressed'],
          sourceType: ['album', 'camera'],
          success (res) {
            // res.tempFilePath可以作为img标签的src属性显示图片
            const msg = res.errMsg.split('chooseImage:')[1]
            Vue.set(vuer.userInfo, 'userPic', res.tempFilePaths)
            wx.showToast({
              title: msg,
              icon: 'success',
              duration: 1500
            })
          },
          fail: function (res) {
            const msg = res.errMsg.split('chooseImage:')[1]
            wx.showToast({
              title: msg,
              icon: 'error',
              duration: 1500
            })
          }
        })
      }
    },
    components: {
      card
    },
    onLoad (res) {
      wx.showShareMenu({
        withShareTicket: true,
        menus: ['shareAppMessage', 'shareTimeline']
      })
    },
    onShareAppMessage (res) {
      return {
        title: '自定义分享标题'
      }
    },
    onShareTimeline (res) {
      return {
        title: '自定义分享标题'
      }
    }
  }
</script>

<style scoped>
  .root-wrap{
    height: 100%;
    background: linear-gradient(#FA4039, #FF8460 30%, transparent 50%, transparent 100%);
  }
  .userpic {
    overflow: hidden;
    padding: 200rpx 0 52rpx 0;
  }
  .user-left{
    width: 104rpx;
    height: 104rpx;
    border-radius: 50%;
    overflow: hidden;
    margin: 0 40rpx 0 0;
    border: 4px solid rgba(255, 255, 255, 0.82);
  }
  .user-left .userpic-img{
    width: 100%;
    height: 100%;
  }
  .user-left,
  .user-right{
    float: left;
    color: white;
  }
  .user-name{
    font-size: 36rpx;
    padding: 7rpx 0 10rpx;
  }
  .user-phone{
    font-size: 28rpx;
  }
  .appointment{
    float: right;
    width: 132rpx;
    height: 48rpx;
    border-radius: 27rpx;
    color: white;
    border: 2rpx solid white;
    margin: 50rpx 0 0;
    font-size: 24rpx;
    text-align: center;
    line-height: 48rpx;
  }
  .vipCard-box{
    width: 686rpx;
    margin: 0 auto;
  }
  .vipCard-txt{
    font-size: 32rpx;
    line-height: 86rpx;
    padding: 0 0 0 28rpx;
    color: white;
  }
  .go-recharge{
    float: right;
    width: 104rpx;
    height: 38rpx;
    line-height: 38rpx;
    border-radius: 38rpx;
    text-align: center;
    font-size: 24rpx;
    background: linear-gradient(to right, #F6CC7E , #D1A632);
    color: #080000;
    margin: 24rpx 28rpx 0 0;
  }
  .vipCard-bottom{
    width: 100%;
    height: 198rpx;
    border-radius: 16rpx;
    background: white;
  }
  .vipCard-bottom ul{
    display: flex;
    justify-content: center;
    padding: 60rpx 0 0;
  }
  .vipCard-bottom ul li{
    font-size: 28rpx;
    text-align: center;
  }
  .vipCard-bottom ul .li-center{
    padding: 0 210rpx;
  }
  .vipCard-bottom ul li p{
    padding: 10rpx 0 0;
    font-size: 24rpx;
  }
  .user-process{
    width: 686rpx;
    height: 168rpx;
    background: white;
    border-radius: 16rpx;
    margin: 28rpx auto 0;
  }
  .user-process ul{
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .user-process ul li{
    font-size: 24rpx;
    text-align: center;
    color: #262626;
    margin: 0 50rpx;
  }
  .user-process ul li p{
    width: 60rpx;
    height: 60rpx;
    margin: 0 auto 10rpx;
    position: relative;
  }
  .user-process ul li p img{
    width: 100%;
    height: 100%;
  }
  .user-process ul li p i{
    position: absolute;
    width: 32rpx;
    height: 32rpx;
    line-height: 32rpx;
    border-radius: 50%;
    background: #EC5151;
    text-align: center;
    font-size: 24rpx;
    color: white;
    top: -13rpx;
    right: -13rpx;
  }
  .user-process .ulpro{
    justify-content: flex-start;
  }
  .user-process .ulpro li{
    margin: 0 40rpx;
  }
  .user-process .ulpro li p{
    width: 72rpx;
    height: 72rpx;
  }
</style>
