<template>
	<newsList :newsList="newsList" @innerClick="navToDetail($event)"/>
</template>

<script>
	import newsList from '@/components/newsList.vue'
	export default {
		components:{
			newsList
		},
		data() {
			return {
            newsList:[]
			}
		},
		methods: {
         getNews(){
			 this.$myRequest({
				 url:`/api/getnewslist`
			 }).then(res=>{
				 if(res.data.status===0){
					 this.newsList = res.data.message
					 // console.log(this.newsList)
				 }
			 })
		 },
		 navToDetail(e){
			 // console.log(e)
			 uni.navigateTo({
			 	url:`/pages/news_detail/news_detail?id=${e}`
			 })
		 }
		},
		onLoad(){
			this.getNews()
		}
	}
</script>

<style lang="scss" scoped>
</style>
