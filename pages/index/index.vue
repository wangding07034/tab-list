<template>
	<view class="page">
		
		<qsTab
		ref="tabs" 
		:tabs="tabs" 
		animationMode="line3" 
		:current="current"
		 @change="tabChange"
		swiperWidth="750">
		</qsTab>
		
		<swiper class="swiper" :current="current"  @change="swiperChange" 
		@transition="transition"
		@animationfinish="animationfinish">
			<swiper-item class="swiper-item" @transition="transition" v-for="(item, index) in tabs" :key="index">
				<indexList :i="index" :type="current"></indexList>
			</swiper-item>
		</swiper>
		
	</view>
</template>

<script>
	import indexList from './list.vue'
	import qsTab from '../../components/QS-tabs/QS-tabs.vue'
	
	export default {
		components: {
			qsTab,
			indexList
		},
		data() {
			return {
				current: 0,
				tabs: [
					{name: '选项1'},
					{name: '选项2'},
					{name: '选项3'},
					{name: '选项4'},
					{name: '选项5'}
				]
			}
		},
		methods:{
			swiperChange(e) {
				this.current = e.detail.current
			},
			
			transition({ detail: { dx } }) {
				this.$refs.tabs.setDx(dx);
			},
			animationfinish({detail: { current }}) {
				this.$refs.tabs.setFinishCurrent(current);
				// this.swiperCurrent = current;
				this.current = current;
			},
			/**
			 * 选显卡切换
			 * */
			tabChange(index) {
				this.current = index
			}
		}
	}
</script>

<style lang="scss" scoped>
	.page {
		width: 100%;
		height: 100%;
	}
	.swiper {
		width: 100%;
		height: 100%;
		.swiper-item {
			width: 100%;
			height: 100%;
		}
	}
</style>