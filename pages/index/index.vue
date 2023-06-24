<template>
    <view class="content">
       我是首页
    </view>
</template>

<script>
    export default {
        data() {
            return {
                text: "Hello JavaEdge"
            }
        },
        onLoad() {

        },
        methods: {
          click() {
            console.log(this.text)
            console.log("text")
          }
        }
    }
</script>

<style>
    .content {
        background-color: red;
    }
</style>