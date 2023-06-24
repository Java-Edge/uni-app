<template>
    <view :class="text" :style="style">
        Hello JavaEdge
    </view>
</template>

<script>
    export default {
        data() {
            return {
                style: "font-size:70px",
                text: "content"
            }
        },
        onLoad() {

        },
        methods: {

        }
    }
</script>

<style>
    .content {
        background-color: red;
    }
</style>