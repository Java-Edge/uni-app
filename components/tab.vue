<template>
  <view class="tab">
    <navigator open-type="switchTab" url="/pages/index/index" class="tab-box">
      首页
    </navigator>
    <navigator open-type="switchTab" url="/pages/follow/follow" class="tab-box">
      朋友
    </navigator>
    <view class="tab-box">
      <view class="iconfont iconjiahao icon-box">
      </view>
    </view>
    <navigator open-type="switchTab" url="/pages/news/news" class="tab-box">
      消息
    </navigator>
    <navigator open-type="switchTab" url="/pages/personal/personal" class="tab-box">
      我
    </navigator>
  </view>
</template>

<script>
export default {
  data() {
    return {};
  }
}
</script>

<style>
.tab {
  height: 50px;
  width: 100%;
  position: fixed;
  bottom: 0;
  left: 0;
  z-index: 20;
}

.tab-box {
  float: left;
  width: 20%;
  color: #FFFFFF;
  background: #000000;
  text-align: center;
  height: 50px;
  line-height: 50px;
  font-size: 20px
}

.icon-box {
  width: 60%;
  height: 30px;
  background: #FFFFFF;
  color: #000000;
  margin: 10px 20%;
  line-height: 30px;
  border-radius: 5px;
  font-size: 15px;
}
</style>
