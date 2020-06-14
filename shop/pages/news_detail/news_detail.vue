<template>
	<view class="news_detail">
		<text>标题：{{detail.title}}</text>
		<view>
			<text>发布时间：{{detail.add_time | formatDate}}</text>
			<text>浏览次数：{{detail.click}}</text>
		</view>
		<text>内容：</text>
		<rich-text :nodes="detail.content"></rich-text>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				id:0,
				detail:''
			}
		},
		filters:{
			formatDate(date){
				let ndate = new Date(date)
				let year = ndate.getFullYear()
				let month = (ndate.getMonth()+1).toString().padStart(2,0)
				let day = ndate.getDay().toString().padStart(2,0)
				return `${year}-${month}-${day}`
			}
		},
		methods: {
			getNewsDetail(){
				this.$myRequest({
					url:`/api/getnew/${this.id}`
				}).then(res=>{
					if(res.data.status === 0){
						this.detail = res.data.message[0]
						console.log(this.detail)
					}
				})
			}
		},
		onLoad(options){
			// console.log(options.id)
			this.id = options.id
			this.getNewsDetail()
		}
	}
</script>

<style lang="scss">
.news_detail{
	font-size: 30rpx;
	padding:0 20rpx;
	margin:20rpx 0;
	&>text:nth-child(1){
		display: block;
		text-align:center;
		font-weight: bold;
	}
	view{
		display: flex;
		justify-content: space-between;
	}
}
</style>
