<template>
	<view class="home">
		<swiper indicator-dots autoplay circular>
			<swiper-item v-for="(item,index) in swipers" :key="item.id">
				<image :src="item.img" :key="item.id"></image>
				</swiper-item>
		</swiper>
		<view class="nav">
			<view class="nav_item" v-for="(item,index) in navs" :key="index" @click="navWhenClick(item.path)">
				<view :class="item.icon" ></view>
				<text>{{item.title}}</text>
			</view>
			
		</view>
		
		<view class="hot_goods">
			<view class="title">
				推荐商品
			</view>
			<goods-list :goodsList="goods" @itemClick="navTo"/>
			
		</view>
	</view>
</template>	

<script>
	import goodsList from '@/components/goodsList'
	export default {
		components:{
			'goods-list':goodsList
		},
		data() {
			return {
				swipers:'',
				goods:'',
				navs:[
					{
						icon:'iconfont icon-ziyuan',
						title:'超市',
						path:'/pages/goods/goods'
					},
					{
						icon:'iconfont icon-tupian',
						title:'图片',
						path:'/pages/pics/pics'
					},
					{
						icon:'iconfont icon-shipin',
						title:'视频',
						path:'/pages/videos/videos'
					},
					{
						icon:'iconfont icon-guanyuwomen',
						title:'关于我们',
						path:'/pages/contact/contact'
					}
				]
			}
		},
		methods: {
          getSwipers(){
			 this.$myRequest({
				 url:'/api/getlunbo'
			 }).then(res=>{
				 this.swipers = res.data.message
				 })
		  },
		  getHotGoods() {
		  	this.$myRequest({
		  		url: '/api/getgoods?pageindex=1'
		  	}).then(res => {
		  		if (res.data.status === 0) {
		  			this.goods = res.data.message
		  		}
		  		// console.log(this.goods)
		  	})
		  },
		  navWhenClick(path){
			  uni.navigateTo({
			  	url:path
			  })
		  },
		  navTo(id){
			  // console.log('test')
			  uni.navigateTo({
			  	url:`/pages/goods_detail/goods_detail?id=${id}`
			  })
		  }
		},
		onLoad(){
			this.getSwipers(),
			this.getHotGoods()
		}
	}
</script>

<style lang="scss" scoped>
	.home{
		swiper{
			width:750rpx;
			height: 380rpx;
			image{
				width:100%;
				height: 100%;
			}
		}
		.nav{
			display: flex;
			.nav_item{
				width:25%;
				text-align: center;
				view{
					width:120rpx;
					height: 120rpx;
					background-color:#8c8baa ;
					border-radius: 60rpx;
					margin:10px auto;
					line-height: 120rpx;
					color: white;
				}
			}
			
			text{
				font-size: 30rpx;
			}
		}
		.hot_goods{
			background-color: #eee;
			margin:10px 0;
			.title{
				height: 50px;
				line-height: 50px;
				color: #2C405A;
				text-align: center;
				letter-spacing: 20px;
			}
		}
	}
</style>
