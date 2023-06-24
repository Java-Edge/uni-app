<template>
    <view class="content">
        {{text}}
        <view class="" v-text="text">

        </view>

        <view class="" v-html="text">

        </view>
    </view>
</template>

<script>
    export default {
        data() {
            return {
                text: '<p>hello JavaEdge</p>'
            }
        },
        onLoad() {

        },
        methods: {

        }
    }
</script>

<style>
</style>