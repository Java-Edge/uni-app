<template>
	<view class="changeList">
		<scroll-view class="scrolly" scroll-y="true" :scroll-into-view="viewId">
			<view class="city-box">
				<view class="box">
					<view class="title">
						<icon class="iconfont icondingwei"></icon>
						当前城市
					</view>
					<view class="currentCity">{{tcity}}</view>
				</view>
				<view class="box">
					<view class="title">
						热门城市
					</view>
					<view class="hotlist">
						<view class="item" v-for="(item,index) of list" :key="index">
							{{item}}
						</view>
					</view>
				</view>
				<view class="box-list" v-for="(cities,index) in city" :key="index">
					<view class="initial" :id="cities.initial">
						{{cities.initial}}
					</view>
					<view 
					class="city-name" 
					v-for="item of cities.list" 
					:key="item.code"
					@click="click(item.name)">
						{{item.name}}
					</view>
				</view>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		props:['city','letter'],
		data() {
			return {
				list:['深圳','北京','上海','成都','广州','重庆','西安','苏州','武汉','杭州','郑州','南京'],
				viewId:'',
				tcity:"北京"
			};
		},
		methods:{
			click(res){
				uni.setStorage({
					key:'city',
					data:res
				})
				uni.getStorage({
					key:'city',
					success: (res) => {
						this.tcity=res.data
					}
				})
				uni.redirectTo({
					url:'/pages/city/city'
				})
			}
		},
		watch:{
			letter(){
				this.viewId=this.letter
			}
		}
	}
</script>

<style>
.changeList{
	width: 100%;
	background: #000000;
	z-index: 19;
	height: 100%;
}
.box{
	background: #222222;
	margin-top: 10px;
	padding:0 5px 20px 5px
}
.title{
	height: 40px;
	line-height: 40px;
	margin-left: 15px;
	color: #FFFFFF;
	font-size: 14px;
}
.currentCity{
	color: #AAAAAA;
	font-size: 15px;
	margin-left: 15px;
	height:30px;
	line-height: 30px;
}
.hotlist{
	width:100%;
	overflow: hidden;	
}
.item{
	width:30%;
	height:28px;
	line-height: 28px;
	font-size: 13.5px;
	float: left;
	background: #333333;
	margin-left:2.5%;
	margin-bottom: 10px;
	text-align: center;
	color: #AAAAAA;
}
.box-list{
	padding: 8px 5px;
}
.initial{
	height: 25px;
	line-height: 25px;
	background: #000000;
	padding-left: 10px;
	color: #666666;
	font-size: 12px;
}
.city-name{
	background: #222222;
	height: 40px;
	line-height: 40px;
	padding-left: 10px;
	color: #AAAAAA;
	font-size: 15px;
}
.scrolly{
	height: 100%;
}

		  
</style>
