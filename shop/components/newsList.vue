<template>
	<view class="news">
		<view class="news_item"  v-for="item in newsList" :key="item.id" @click="navigator(item.id)">
			<image :src="item.img_url" alt="这是图片" ></image>
			<view class="right">
				<view class="tit">
					{{item.title}}
				</view>
				<view class="info">
					<text>发布时间: {{item.add_time |formatDate}}</text>
					<text>浏览次数: {{item.click}}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:['newsList'],
		data() {
			return {

			};
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
			test() {
				console.log(this.newsList)
			},
			navigator(id){
				// console.log(id)
				this.$emit('innerClick',id)
			}
			
		},
		onLoad(){
			// console.log(this.newsList[0].click)
		}
	}
</script>

<style lang="scss">
	.news {
		.news_item {
			display: flex;
			padding: 20rpx;
			border-bottom: 1px solid red;

			image {
				width: 200rpx;
				min-width: 200rpx;
				height: 150rpx;
				min-height: 150rpx;
			}

			.right {
				margin-left: 15rpx;
				display: flex;
				flex-direction: column;
				justify-content: space-between;

				.tit {
					font-size: 33rpx;
				}

				.info {
					font-size: 24rpx;

					text:nth-child(2) {
						margin-left: 20rpx;
					}
				}
			}
		}
	}
</style>
