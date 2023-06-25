<template>
  <!-- 包含一个视频组件和一个图标组件。视频组件用于显示一个视频，图标组件则用于实现点击播放功能 -->
  <!-- `<view>`：是小程序中用于呈现视图的元素，类似于HTML中的`<div>`标签。-->
  <!--      6. `objectFit="cover"`：定义视频显示样式，cover表示将视频铺满整个视频容器，保持视频原始比例，超出部分会被裁剪。-->
  <!--      7. `loop="true"`：表示视频循环播放。-->
  <!--      8. `:src="'http://192.168.10.59:80/video/'+item.src"`：表示视频的资源路径，动态绑定了一个item.src的值，将此值拼接到资源路径中。-->
  <!--      9. `:controls="false"`：表示禁用视频的控件（播放、暂停、进度条等）。-->
  <!--      10. `@click="PlayerTo(list)"`：表示点击视频时触发一个事件PlayerTo，传递参数为list。-->
  <!--      11. `<cover-view>`：是小程序中用于在视图上添加遮罩层和图标的组件。-->
  <!--        13. `@click="click"`：表示点击图标时触发一个事件click。-->
  <view class="followPlayer">
    <video
        id="myVideo"
        class="video"
        objectFit="cover"
        loop="true"
        :src="'http://192.168.10.59:80/video/'+item.src"
        :controls="false"
        @click="PlayerTo(list)"
    >
      <cover-view class="iconfont iconbofang icon" @click="click"></cover-view>
    </video>
  </view>
</template>

<script>
export default {
  props: ['item', 'index', 'list'],
  data() {
    return {
      Play: false
    };
  },
  onReady() {
    this.videoContext = uni.createVideoContext('myVideo', this)
    if (this.index === 0) {
      this.play()
    }
  },
  methods: {
    play() {
      if (this.Play === false) {
        this.videoContext.play()
      }
      this.Play = true
    },
    pause() {
      if (this.Play === true) {
        this.videoContext.pause()
      }
      this.Play = false
    },
    click() {
      if (this.Play === true) {
        this.videoContext.pause()
        this.Play = false
      } else {
        this.videoContext.play()
        this.Play = true
      }
    },
    PlayerTo(res) {
      uni.setStorage({
        key: 'videoList',
        data: res
      })
      uni.navigateTo({
        url: '/pages/player/player'
      })
    }
  },


}
</script>

<style>
.followPlayer {
  height: 100%;
  width: 100%;
}

.video {
  width: 80%;
  height: 100%;
  z-index: 19;
  position: relative;
}

.icon {
  position: absolute;
  bottom: 10px;
  right: 10px;
  color: #FFFFFF;
  font-size: 20px;
}
</style>
