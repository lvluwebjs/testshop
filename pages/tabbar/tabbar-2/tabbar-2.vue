<template>
	<view class="content">
		<view class="scroll-content">
			<scroll-view scroll-with-animation="true" :scroll-top="scrollTop" scroll-y="true" class="scroll-box">
				<view class="list-item" v-for="item in list" :key='item.id'
					:class="[current===item.id?'activeCurrnet':0]" :data-index="item.id" @click="changeCurrent($event)">
					{{item.title}}
				</view>
			</scroll-view>
		</view>

		<view class="content-left">
			<view class="content-shop-one" v-if="current==0">
				1
			</view>
			<view class="content-shop-two" v-if="current==1">
				2
			</view>
			<view class="content-shop-three" v-if="current==2">
				3
			</view>
			<view class="content-shop-four" v-if="current==3">
				4
			</view>
			<view class="content-shop-five" v-if="current==4">
				5
			</view>
			<view class="content-shop-six" v-if="current==5">
				6
			</view>
			<view class="content-shop-seven" v-if="current==6">
				7
			</view>
			<view class="content-shop-eight" v-if="current==7">
				8
			</view>
			<view class="content-shop-nine" v-if="current==8">
				9
			</view>
		</view>
	</view>
</template>

<script>
	import list from '../../../static/dataJs/list.js';
	// console.log(list.listData)
	export default {
		data() {
			return {
				current: 0,
				scrollTop: 0,
				moveHeight: 0,
				list: list.listData,
			}
		},
		onLoad() {
			uni.getSystemInfo({
				success: (res) => {
					//初始化计算视口高度与宽度
					this.moveHeight = res.windowHeight
					// console.log(this.moveHeight)
				}
			})
		},
		methods: {
			changeCurrent(e) {
				this.current = e.currentTarget.dataset.index;
				var num = parseInt(this.moveHeight / 46)
				//当e.currentTarget.dataset.index - (num-2) / 2为负数的时候列表不滚动，直到值为正数时候才开始滚动，横向列表也是一个道理
				if ((e.currentTarget.dataset.index - num / 2) === 1) {
					this.scrollTop = (e.currentTarget.dataset.index - num / 2) * this.moveHeight / num
					console.log(this.scrollTop)
				} else {
					this.scrollTop = (e.currentTarget.dataset.index - num / 2) * this.moveHeight / num
					// console.log(this.scrollTop)
				}


			}
		}
	}
</script>

<style scoped>
	.content {
		display: flex;
		flex-direction: row;

	}

	.scroll-content {
		width: 172rpx;
	}

	.scroll-box {
		position: fixed;
		width: 172rpx;
		height: 100%;

	}

	.list-item {
		background-color: #f8f8f8;
		height: 92rpx;
		text-align: center;
		line-height: 92rpx;
		font-size: 28rpx;
		color: #333;


	}

	.activeCurrnet {
		border-left: 4px solid red;
		background-color: #fff;
		box-sizing: border-box;
		color: red;

	}

	.content-left {
		flex: 1;
	}
</style>
