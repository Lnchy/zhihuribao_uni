<template>
	<view class="content">
		
        <view class="uni-list">
        	<view class="uni-list-cell" hover-class="uni-list-cell-hover" v-for="(item,index) in list.stories" :key="index" @tap="openInfo(item.id)">
        		<view class="uni-media-list">
        			<image class="uni-media-list-logo" :src="item.images"></image>
        			<view class="uni-media-list-body">
        				<view class="uni-media-list-text-top">{{item.title}}</view>
        			</view>
        		</view>
        	</view>
        </view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: []
			}
		},
		onLoad() {
			uni.request({
				url:'https://news-at.zhihu.com/api/4/news/latest',
				method:'get',
				data:{},
				success: res => {
					this.list = res.data
				},
				fail: () => {},
				complete: () => {}
			})
		},
		methods: {
			openInfo(id) {
				uni.navigateTo({
					url: '../info/info?id=' + id
				});
			}
		}
	}
</script>

<style>
</style>
