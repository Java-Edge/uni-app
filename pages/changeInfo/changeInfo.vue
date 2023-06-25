<template>
  <view class="changeInfo">
    <view class="nav-box">
      <view class="title">编辑个人资料</view>
      <navigator
          open-type="switchTab"
          url="/pages/personal/personal"
          class="iconfont iconfanhui icon-nav"
      ></navigator>
    </view>
    <view class="box">
      <view class="img-box">
        <image
            class="img"
            :src="src"
            @click="chooseImg"
        ></image>
        <view class="text">点击更换头像</view>
      </view>
    </view>
    <view class="info-box">
      <navigator open-type="redirect" url="/pages/modify/modify?title=userName" class="text-box">
        <view class="left">昵称</view>
        <view class="iconfont iconchangyongicon- icon-box"></view>
        <view class="right">{{ user.userName }}</view>
      </navigator>
      <navigator open-type="redirect" url="/pages/modify/modify?title=douyinId" class="text-box">
        <view class="left">抖音号</view>
        <view class="iconfont iconchangyongicon- icon-box"></view>
        <view class="right">{{ user.userId }}</view>
      </navigator>
      <navigator open-type="redirect" url="/pages/modify/modify?title=introduction" class="text-box">
        <view class="left">简介</view>
        <view class="iconfont iconchangyongicon- icon-box"></view>
        <view class="right">{{ user.introduction }}</view>
      </navigator>

      <!-- 小程序的选择器组件，可在页面让用户选择一个学校。
      一个选择器组件，用户可以通过选择器选择一个学校，并且选择结果会被显示在页面 -->
      <!--      <picker> 是选择器组件的标签，通过 range` 属性设置可供选择的数据范围，即 `school` 数组
        同时通过 `@change` 事件绑定事件处理函数 `bindSchoolChange`。-->
      <picker :range="school" @change="bindSchoolChange">
        <!-- `<view>` 是一个视图容器标签，用来包含选择器的各个元素。-->
        <!-- `class` 属性是 CSS 样式类，用来为每个元素设置样式。-->
        <view class="text-box">
          <view class="left">学校</view>
          <!-- `iconfont iconchangyongicon- icon-box` 是字体图标，呈现一个选中状态的图标在选择器右侧。-->
          <view class="iconfont iconchangyongicon- icon-box"></view>
          <!-- `{{user.school}}` 小程序表达式，显示选择器选择的结果 -->
          <view class="right">{{ user.school }}</view>
        </view>
      </picker>
      <picker :range="sex" @change="bindSexChange">
        <view class="text-box">
          <view class="left">性别</view>
          <view class="iconfont iconchangyongicon- icon-box"></view>
          <view class="right">{{ user.sex }}</view>
        </view>
      </picker>
      <picker mode="date" :value="user.birthday" @change="bindDateChange">
        <view class="text-box">
          <view class="left">生日</view>
          <view class="iconfont iconchangyongicon- icon-box"></view>
          <view class="right">{{ user.birthday }}</view>
        </view>
      </picker>
      <picker mode="region" @change="bindCityChange">
        <view class="text-box">
          <view class="left">地区</view>
          <view class="iconfont iconchangyongicon- icon-box"></view>
          <view class="right">{{ user.city }}</view>
        </view>
      </picker>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      src: '../../static/img/author.jpg',
      user: {
        userName: "JavaEdge",
        userId: "123435",
        introduction: "我爱Java",
        school: "",
        sex: "",
        birthday: '',
        city: ''
      },
      school: ['清华大学', '北京大学', "复旦大学", '南京大学'],
      sex: ['男', '女']
    }
  },
  methods: {
    chooseImg() {
      uni.chooseImage({
        count: 1,
        sourceType: ['album'],
        sizeType: ['original', 'compressed'],
        success: (res) => {
          this.src = res.tempFilePaths
        }
      })
    },
    /**
     * 处理下拉列表的选择事件：
     *
     * 因此，当用户在下拉列表中选择了学校时，该方法会将选择的学校保存到本地缓存中，并更新Vue实例中的用户学校属性。
     * @param e 事件参数，包含了被选择的选项的值。
     */
    bindSchoolChange(e) {
      // 将用户的学校属性更新为选中的选项的值。`this`指Vue实例
      this.user.school = this.school[e.target.value]
      // 将数据存储到本地缓存
      uni.setStorage({
        // 存储的键名
        key: 'school',
        // 存储的数据，这里存储的是用户选择的学校
        data: this.school[e.target.value],

      })
    },
    bindSexChange(e) {
      this.user.sex = this.sex[e.target.value]
      uni.setStorage({
        key: 'sex',
        data: this.sex[e.target.value],

      })
    },
    bindDateChange(e) {
      this.user.birthday = e.target.value
      uni.setStorage({
        key: 'birthday',
        data: e.target.value,

      })
    },
    bindCityChange(e) {
      this.user.city = e.target.value[0]
      uni.setStorage({
        key: 'city',
        data: e.target.value[0]
      })
    }
  },
  onLoad() {
    uni.getStorage({
      key: 'userName',
      success: (res) => {
        this.user.userName = res.data
      }
    }),
        uni.getStorage({
          key: 'userId',
          success: (res) => {
            this.user.userId = res.data
          }
        }),
        uni.getStorage({
          key: 'intrduction',
          success: (res) => {
            this.user.introduction = res.data
          }
        }),
        uni.getStorage({
          key: 'school',
          success: (res) => {
            this.user.school = res.data
          }
        }),
        uni.getStorage({
          key: 'sex',
          success: (res) => {
            this.user.sex = res.data
          }
        }),
        uni.getStorage({
          key: 'birthday',
          success: (res) => {
            this.user.birthday = res.data
          }
        }),
        uni.getStorage({
          key: 'city',
          success: (res) => {
            this.user.city = res.data
          }
        })
  }
}
</script>

<style>
.changeInfo {
  width: 100%;
  height: 100%;
  background: #000000;
}

.nav-box {
  height: 50px;
  position: relative;
  margin: 0 auto;
  padding-top: 30px;
}

.title {
  text-align: center;
  color: #FFFFFF;
  font-size: 18px;
}

.icon-nav {
  position: absolute;
  top: 30px;
  left: 10px;
  color: #FFFFFF;
}

.box {
  width: 100%;
  height: 150px;
  margin: 0 auto;
  border-top: 1px solid #333333;
  border-bottom: 1px solid #333333;
}

.img-box {
  text-align: center;
}

.img {
  margin-top: 20px;
  width: 70px;
  height: 70px;
  border-radius: 50%;
}

.text {
  margin-top: 13px;
  color: #999999;
  font-size: 13px;
}

.info-box {
  padding: 0 10px;
}

.text-box {
  width: 100%;
  height: 52px;
  line-height: 52px;

}

.left {
  float: left;
  font-size: 15px;
  color: #FFFFFF;
}

.right {
  float: right;
  font-size: 15px;
  margin-right: 7px;
  color: #999999;
}

.icon-box {
  float: right;
  font-size: 15px;
  color: #999999;
  width: 10px;
}
</style>
