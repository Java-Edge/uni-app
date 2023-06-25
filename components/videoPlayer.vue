<template>
	<view class="videoPlayer">
		<video 
		id="myVideo" 
		class="video" 
		:controls="false" 
		:loop="true" 
		:src="'http://192.168.11.164:80/video/'+video.src" 
		:autoplay="autoplay"
		@click="click"
		>
		</video>
		
	</view>
</template>

<script>
	var timer=null
	export default {
		props:['video','index'],
		data() {
			return {
				play:false,
				dblClick:false,
				autoplay:false
			};
		},
		onReady(){
			this.videoContext=uni.createVideoContext('myVideo',this)
		},
		methods:{
			click(){
				clearTimeout(timer)
				this.dblClick=!this.dblClick
				timer=setTimeout(()=>{
					if(this.dblClick){
						//单击
						if(this.play===false){
							this.playThis()
						}else{
							this.pause()
						}
					}else{
						//双击
						this.$emit('changeClick')
					}
					this.dblClick=false
				},300)
			},
			player(){
				//从头播放视频
				if(this.play===false){
					this.videoContext.seek(0)
					this.videoContext.play()
					this.play=true
				}
			},
			pause(){
				//暂停视频
				if(this.play===true){
					this.videoContext.pause()
					this.play=false
				}
			},
			playThis(){
				//播放当前视频
				if(this.play===false){
					this.videoContext.play()
					this.play=true
				}
			},
			atuo(){
				//首个视频自动播放
				if(this.index===0){
					this.autoplay=true
				}
			}
		},
		created() {
			this.atuo()
		}
	}
	
</script>

<style>
.videoPlayer{
	height: 100%;
	width:100%;
}
.video{
	height: 100%;
	width:100%;
	z-index: 19;
}
</style>
