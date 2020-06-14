<template>
	<view class="pics">
		<scroll-view class="left" scroll-y>
			<view :class="active === index?'active':''" v-for="(item,index) in imgCategory" :key="item.id" @click="change(index,item.id)">
				{{item.title}}
			</view>
		</scroll-view>
		<scroll-view scroll-y="true" class="right">
			<view class="item" v-for="item in imgs" :key="item.id">
				<image @click="preview(item.img_url)" :src="item.img_url" ></image>
				<text>{{item.title}}</text>
			</view>
			<text v-if="imgs.length===0">暂无数据</text>
		</scroll-view>
	</view>
</template>

<script >
	export default {
		data() {
			return {
				imgCategory:'',
				imgs:'',
				active:0
			}
		},
		methods: {
			getPics(){
				this.$myRequest({
					url:'/api/getimgcategory'
				}).then(res=>{
					if(res.data.status===0){
						this.imgCategory = res.data.message
						this.change(0,this.imgCategory[0].id) //一进来时第一个标签的右侧内容
					}
					
				})
			},
			change(index,id){
				this.active = index
				// console.log(id)
				this.$myRequest({
					url:`/api/getimages/${id}`
				}).then(res=>{
					if(res.data.status===0){
						this.imgs = res.data.message
					}
					console.log(this.imgs)
				})
			},
			preview(current){
				const urls = this.imgs.map(i=>{
					return i.img_url
				})
				// console.log(cur)
				uni.previewImage({
					current,
				    urls
				})
			}
		},
		onLoad(){
			this.getPics()
		}
	}
</script>

<style lang="scss" scoped> 
page{
	height:100%;
}
.pics{
	height:100%;
	display: flex;
	.left{
		width:200rpx;
		height:100%;
		border-right: 2px solid #eee;
		view{
			height:60px;
			line-height: 60px;
			color: #333;
			text-align: center;
			font-size: 30rpx;
			border-top:2px solid #eee;
		}
	}
	.right{
		height: 100%;
		width:550rpx;
		margin:10rpx auto;
		.item{
			image{
				width:530rpx;
				height:530rpx;
				border-radius: 8rpx;
			}
			text{
				font-size: 30rpx;
				line-height: 60rpx;
			}
		}
	}
	.active{
		background-color: red;
		color:#fff;
	}
}
</style>
