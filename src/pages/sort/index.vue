<template>
  <div class="root-wrap">
    <h2 class="sort-title txt-center">分类</h2>
    <div class="item-wrap">
      <div class="item-left txt-center">
        <ul>
          <li 
            v-for="(item, index) in menu"
            :key="index"
            :class="{active: item.isActive}"
            @click="onTab(index)"
          >
            {{item.name}}
          </li>
        </ul>
      </div>
      <div class="item-right">
        <div v-for="(value, index) in activeChild" :key="index">
          <div class="swiper-box">
            <Swiper :images="value.child.banners"/>
          </div>
          <div class="item-box" v-for="(itm, i) in value.child.items" :key="i">
            <h3 class="item-title">{{itm.title}}</h3>
            <ul>
              <li v-for="(lis, k) in itm.list" :key="k" :class="{'no-margin': (k+1)%3 == 0}" >
                <a :href="lis.url">
                  <img :src="lis.img">
                  <p>{{lis.name}}</p>
                </a>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import Vue from 'vue'
  import card from '@/components/card'
  import Swiper from '@/components/swiper'

  export default {
    data () {
      let tabData = {
        menu: [
          {
            name: '热门推荐',
            isActive: true,
            child: {
              banners: [
                {
                  img: '/static/images/vipcardbg.png',
                  url: '/'
                },
                {
                  img: '/static/images/head.jpg',
                  url: '/'
                }
              ],
              items: [
                {
                  title: '分类标题111',
                  list: [
                    {
                      name: '常用配件111',
                      url: '/',
                      img: '/static/images/head.jpg'
                    },
                    {
                      name: '常用配件111',
                      url: '/',
                      img: '/static/images/head.jpg'
                    }
                  ]
                },
                {
                  title: '分类标题111',
                  list: [
                    {
                      name: '常用配件111',
                      url: '/',
                      img: '/static/images/head.jpg'
                    },
                    {
                      name: '常用配件111',
                      url: '/',
                      img: '/static/images/head.jpg'
                    }
                  ]
                }
              ]
            }
          },
          {
            name: '生活精品',
            isActive: false,
            child: {
              banners: [
                {
                  img: '/static/images/vipcardbg.png',
                  url: '/'
                },
                {
                  img: '/static/images/head.jpg',
                  url: '/'
                }
              ],
              items: [
                {
                  title: '分类标题222',
                  list: [
                    {
                      name: '常用配件222',
                      url: '/',
                      img: '/static/images/head.jpg'
                    }
                  ]
                },
                {
                  title: '分类标题222',
                  list: [
                    {
                      name: '常用配件222',
                      url: '/',
                      img: '/static/images/head.jpg'
                    },
                    {
                      name: '常用配件222',
                      url: '/',
                      img: '/static/images/head.jpg'
                    },
                    {
                      name: '常用配件222',
                      url: '/',
                      img: '/static/images/head.jpg'
                    },
                    {
                      name: '常用配件222',
                      url: '/',
                      img: '/static/images/head.jpg'
                    }
                  ]
                }
              ]
            }
          },
          {
            name: '常规保养',
            isActive: false,
            child: {
              banners: [
                {
                  img: '/static/images/vipcardbg.png',
                  url: '/'
                },
                {
                  img: '/static/images/head.jpg',
                  url: '/'
                }
              ],
              items: [
                {
                  title: '分类标题333',
                  list: [
                    {
                      name: '常用配件333',
                      url: '/',
                      img: '/static/images/head.jpg'
                    }
                  ]
                },
                {
                  title: '分类标题333',
                  list: [
                    {
                      name: '常用配件333',
                      url: '/',
                      img: '/static/images/head.jpg'
                    },
                    {
                      name: '常用配件333',
                      url: '/',
                      img: '/static/images/head.jpg'
                    }
                  ]
                },
                {
                  title: '分类标题333',
                  list: [
                    {
                      name: '常用配件333',
                      url: '/',
                      img: '/static/images/head.jpg'
                    }
                  ]
                }
              ]
            }
          }
        ]
      }
      return tabData
    },
    computed: {
      activeChild: function () {
        return this.menu.filter(function (menu) {
          return menu.isActive
        })
      }
    },
    methods: {
      onTab (index) {
        let menus = this.menu
        // this.$children.current = 0
        this.$emit('current', 0)
        for (let i = 0; i < menus.length; i++) {
          Vue.set(menus[i], 'isActive', false)
        }
        Vue.set(menus[index], 'isActive', true)
      }
    },
    components: {
      card,
      Swiper
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
    color: #262626;
    background: white;
    position: relative;
  }
  .sort-title{
    height: 44rpx;
    font-size: 32rpx;
    padding: 115rpx 0 0;
  }
  .item-wrap{
    display: flex;
    position: absolute;
    width: 100%;
    top: 159rpx;
    bottom: 0;

  }
  .item-left{
    flex: 2.5;
    color: black;
    overflow-y: auto;
    background: #F5F5F5;
  }
  .item-right{
    flex: 8;
    overflow-y: auto;
  }
  .item-left ul li{
    height: 112rpx;
    line-height: 112rpx;
    font-size: 28rpx;
    background: #F5F5F5;
    /* border-top-right-radius: 10rpx; */
    /* border-bottom-right-radius: 10rpx; */
  }
  .item-left ul .active{
    font-size: 36rpx;
    background: white;
  }
  .swiper-box{
    width: 510rpx;
    height: 172rpx;
    margin: 30rpx 0 0 26rpx;
    border-radius: 16rpx;
    overflow: hidden;
  }
  .item-box{
    width: 510rpx;
    margin: 0 0 0 26rpx;
  }
  .item-title{
    height: 84rpx;
    line-height: 84rpx;
    font-size: 24rpx;
    color: #A2A2A2;
    border-bottom: 2rpx solid #CFCFCF;
    margin: 0 0 26rpx;
  }
  .item-box ul{
    overflow: hidden;
  }
  .item-box ul li{
    float: left;
    width: 152rpx;
    margin: 0 26rpx 0 0;
  }
  .item-box ul .no-margin{
    margin: 0;
  }
  .item-box ul li img{
    width: 152rpx;
    height: 152rpx;
    border-radius: 16rpx;
  }
  .item-box ul li p{
    height: 66rpx;
    line-height: 66rpx;
    font-size: 18rpx;
    color: black;
  }
</style>
