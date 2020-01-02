<template>
	<MeScroll :up="up" :down="down" @up="upFn" :fixed="false" @down="downFn" @init="initMeScroll">
		<view class="item" v-for="(item,index) in list" :key="index">{{index+1}}</view>
	</MeScroll>
</template>

<script>
	import MeScroll from '../../components/mescroll-uni/mescroll-uni.vue'
	export default {
		components:{
			MeScroll
		},
		props: {
			type: Number,
			i: Number
		},
		data() {
			return {
				total: 30,
				isInit: false, // 是否初始化
				list: [], // 列表数据
				meScroll: null, // meScroll 对象
				// 上拉配置参数
				up: {
					auto: false,
					page: {
						page: 0,
						size: 10
					}
				},
				// 下拉配置参数
				down: {
					auto: false
				}
			}
		},
		
		watch:{
			type(val) {
				if(!this.isInit && val === this.i) {
					this.meScroll.resetUpScroll()
				}
			}
		},
		
		mounted() {
			if(!this.isInit && this.i === 0) {
				this.meScroll.resetUpScroll()
			}
		},
		
		onLoad() {

		},
		methods: {
			
			/**
			 * mescroll 初始化组件
			 * */ 
			initMeScroll(meScroll) {
				this.meScroll = meScroll
			},
			
			/**
			 * 上拉回调
			 * */
			upFn(meScroll) {
				setTimeout(() => {
					let arr = [1,1,1,1,1,1,1,1,1,1]
					this.list = [...this.list,...arr]
						meScroll.endBySize(arr.length, this.total)
				}, 1000)
			},
			
			/**
			 * 下拉回调
			 * */
			downFn(meScroll) {
				this.list = []
				meScroll.resetUpScroll() // 重置列表为第一页 (自动执行 page.num=1, 再触发upCallback方法 )
			}
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}
	
	.item {
		box-sizing: border-box;
		height: 200upx;
		width: 100%;
		border: 1px solid red;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
