<template>
  <view class="player">

    <view class="iconfont iconfanhui icon-fanhui">
    </view>
    <view class="footer">
      留下你精彩评论吧
    </view>

    <video-list :list="list"></video-list>

  </view>
</template>

<script>
import videoList from '../../components/videoList.vue'

export default {
  components: {
    videoList
  },
  data() {
    return {
      list: []
    }
  },
  methods: {},
  onLoad() {
    uni.getStorage({
      key: 'videoList',
      success: (res) => {
        this.list = res.data
      }
    })
  }
}
</script>

<style>
.player {
  height: 100%;
  width: 100%;
  background: #000000;
  position: relative;
}

// 返回按钮
.icon-fanhui {
  z-index: 21;
  color: #FFFFFF;
  font-size: 17px;
  position: absolute;
  top: 30px;
  left: 10px;
}

.footer {
  z-index: 21;
  position: absolute;
  bottom: 20px;
  left: 10px;
  font-size: 16px;
  color: #444444;
}
</style>
