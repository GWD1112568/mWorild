<template>
  <swiper 
    class="swiper"
    :indicator-dots="indicatorDots"
    :autoplay="autoplay"
    :interval="interval"
    :duration="duration"
    :circular="circular"
    :current="current"
  >
    <block v-for="(item, index) in images" :key="index">
      <a :href="item.url">
        <swiper-item>
          <image :src="item.img" class="slide-image" mode="aspectFill"/>
        </swiper-item>
      </a>
    </block>
  </swiper> 
</template>

<script>
export default {
  props: {
    images: {
      type: Array
    }
  },
  data () {
    return {
      current: 0,
      indicatorDots: true,
      autoplay: true,
      interval: 3000,
      duration: 500,
      circular: true
    }
  }
}
</script>

<style scoped>
.swiper {
  height: 100%;
  width: 100%;
}
image {
  height: 100%;
  width: 100%;
}
</style>