<template>
	<view class="goods_detail">
		<swiper :indicator-dots="true"  >
			<swiper-item v-for="(item,index) in swipers" :key="index" >
				<image :src="item.src" mode=""></image>
			</swiper-item>
		</swiper>
		<view class="box1">
			<view class="price">
				<text>{{info.sell_price}}</text>
				<text>{{info.market_price}}</text>
			</view>
			<view class="goods_name">
				{{info.title}}
			</view>
		</view>
		<view class="line"></view>
		<view class="box2">
			<view>货号:{{info.goods_no}}</view>
			<view>库存:{{info.stock_quantity}}</view>
		</view>
		<view class="box3">
			<view class="tit">详情内容</view>
			<rich-text :nodes="detail"></rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				id:0,
				swipers:'',
				info:'',
				detail:''
			}
		},
		methods: {
			getSwipers(){
				this.$myRequest({
					url:`/api/getthumimages/${this.id}`
				}).then(res=>{
					if(res.data.status ===0){
						this.swipers = res.data.message
					}
				})
			},
			getDetail(){
				this.$myRequest({
					url:`/api/goods/getinfo/${this.id}`
				}).then(res=>{
					if(res.data.status === 0){
						this.info = res.data.message[0]
					}
				})
			},
			getContent(){
				this.$myRequest({
					url:`/api/goods/getdesc/${this.id}`
				}).then(res=>{
					if(res.data.status === 0){
						this.detail = res.data.message[0].content
						// console.log(this.detail)
					}
				})
			}
		},
		onLoad(options){
			this.id = options.id
			this.getSwipers()
			this.getDetail()
			this.getContent()
		}
	}
</script>

<style lang="scss" scoped>
.goods_detail{
	padding:10rpx;
	swiper{
		height:700rpx;
		image{
			height:100%;
			width: 100%;
		}
	}
	.price{
		color: red;
		font-size: 36rpx;
		margin: 20rpx 0 5rpx 0;
		text:nth-child(2){
			color: #ccc;
			font-size: 28rpx;
			margin-left: 17rpx;
			text-decoration: line-through;
		}
	}
	.goods_name{
		font-size: 32rpx;
		line-height: 60rpx;
	}
	.line{
		height:10rpx;
		width:750rpx;
		background-color: #eee;
	}
	.gomeImgLoad{
		width:750rpx!important;
	}
}
.box2{
	
}
.box3{
	
}
</style>
