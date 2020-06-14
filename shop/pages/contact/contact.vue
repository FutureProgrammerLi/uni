<template>
	<view>
		这是联系我们页面
		<map :longitude="longitude" :latitude="latitude" :markers="markers"></map>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				longitude:113.390785,
				latitude:22.940209,
				markers:[
					{
						longitude:113.390785,
						latitude:22.940209,
						iconPath:'../../static/icon/news.png',
						width:30,
						height:30
					}
				]
			}
		},
		methods: {
			
		}
	}
</script>

<style>
map{
	height:750rpx;
	width:750rpx;
}
</style>
