<template>
	<view>
		{{ news.body }}
	</view>
</template>

<script>
	export default {
		data() {
			return {
				news: {
					body: ''
				}
			}
		},
		onLoad(option){
			uni.request({
				url: 'https://news-at.zhihu.com/api/4/news/' + option.id,
				method:'get',
				data:{},
				success: res => {
					this.news = res.data
					console.log(this.news)
					var body = this.news.body;
					body = body.replace('查看知乎讨论', '');
					body = body.replace('<script type=\“text\/javascript\”>window.daily=true<\/script>', '');
					body = body.substr(body.indexOf("<p>"));
					this.news.body = body;
					uni.setNavigationBarTitle({
						title:this.news.title
					})
				},
				fail: () => {},
				complete: () => {}
			})
		}
	}
	
</script>

<style>

</style>
