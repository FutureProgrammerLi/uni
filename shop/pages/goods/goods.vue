<template>
	<view class="top">
		<goodsList @itemClick="navTo" :goodsList="goods" />
		<view v-if="reachBottom" class="bottom">
			加载完毕
		</view>
	</view>
</template>

<script>
	import goodsList from '@/components/goodsList.vue'
	export default {
		components:{
			goodsList
		},
		data() {
			return {
				goods:'',
				pageIndex:1,
				reachBottom:false
			}
		},
		methods: {
			getHotGoods(callback) {
				this.$myRequest({
					url: `/api/getgoods?pageindex=${this.pageIndex}`
				}).then(res => {
					// console.log(res)
					if (res.data.status === 0) {
						this.goods = [...this.goods,...res.data.message]
					}
					callback && callback()
					// console.log(this.goods)
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
			this.getHotGoods()
		},
		onReachBottom(){
			if(this.goods.length<this.pageIndex * 10) return this.reachBottom = true     //极其不方便
			this.pageIndex++
			this.getHotGoods()
		},
		onPullDownRefresh(){
			this.pageIndex = 1
			this.goods = []
			this.reachBottom = false
			setTimeout(this.getHotGoods(()=>{
				uni.stopPullDownRefresh()
			}),2000)
		}
	}
</script>

<style scoped>
.top{
	background-color: #eee;
}
.bottom{
	width:100%;
	height:50px;
	line-height: 50px;
	text-align: center;
	font-size:30rpx;
}
</style>
