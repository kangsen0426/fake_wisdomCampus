<template>
	<view class="content">
		<view class="header">

			<view class="l_box">
				<view class="left" @tap="goBack">
					<i class="iconfont icon-jiantou-copy"></i>
				</view>
				
				<view class="title">请假</view>
			</view>

			<view class="h_right" @tap="addVacate">
				<i class="iconfont icon-jiahao"></i>
			</view>

		</view>

		<view class="scroll_wrap">

			<!-- <scroll-view class="scroll"  refresher-enabled refresher-default-style="back"
				refresher-background="#EEEEEE" :refresher-triggered="refresherTriggered"
				@refresherrefresh="refresherrefresh" scroll-y="true"> -->

				<view v-if="vacateList.length" class="scroll_item" @tap="toDetail(item)" v-for="(item,index) in vacateList" :keys="index">

					<view class="left">
						<view class="top">
							<view class="type">{{item.vacateType}}</view>
							<view v-if="item.leaveSchool && !item.leaveprovinces && !item.leaveCity" class="state">需要离校 已销假</view>
							<view v-else-if="item.leaveSchool && item.leaveprovinces && !item.leaveCity" class="state">需要出市 已销假</view>
							<view v-else class="state">需要出省 已销假</view>
						</view>
						<view class="bottom">
							<span>{{item.timeDifference}}({{item.sliceTime1}}~{{item.sliceTime2}})</span>
						</view>
					</view>
					<view class="right">
						<i class="iconfont icon-jiantou"></i>
					</view>
				</view>
				
				
				<view v-if="!vacateList.length" class="empty">
					<span>什么也没有~</span>
				</view>


			<!-- </scroll-view> -->
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				refresherTriggered: false,
				vacateList:[]
			};
		},
		onShow(){
			
			//获取所有请假条
			
			let vacateList = uni.getStorageSync("vacateData") || []
			
			console.log(vacateList)
		
			this.vacateList = vacateList
			
		},
		methods: {
			goBack() {
				uni.navigateTo({
					url:"../index/index"
				})
			},

			toDetail(data) {
				console.log(data)
				uni.navigateTo({
					url:`../vacateDetail/vacateDetail`,
					success() {
						uni.$emit('vacateDetail',data)
					}
				})
			},
			
			refresherrefresh() {

				console.log("chufa")
				this.refresherTriggered = true


				setTimeout(() => {
					this.refresherTriggered = false
				}, 2000)


			},
			addVacate(){
				uni.navigateTo({
					url:"../createVacate/createVacate"
				})
			}
		},
		onPullDownRefresh() {

			setTimeout(() => {
				uni.stopPullDownRefresh()
			}, 2000)
		},





	}
</script>

<style lang="less">
	.content {
		padding-top: 90rpx;

		.header {
			box-sizing: content-box;
			position: fixed;
			height: 70rpx;
			top: 0;
			left: 0;
			right: 0;
			padding: 0rpx 40rpx;
			padding-top: 80rpx;
			display: flex;
			justify-content: space-between;
			// align-items: center;
			background-color: #EEEEEE;
			// background-color: red;
			
			.l_box{
				display: flex;
				align-items: center;
			}
			
			.left {

				i {
					font-size: 22rpx;
					
				}

				margin-right: 40rpx;
			}

			.h_right {
				// position: absolute;
				// right: 40rpx;
				// float: right;

			}

			.title {
				font-size: 32rpx;
				// font-weight: 600;
			}


		}


		.scroll_wrap {
			width: 100%;
			// height: calc(100vh - 180rpx);
			padding: 0 20rpx;
			padding-top: 70rpx;
			padding-bottom: 40rpx;
			background-color: #EEEEEE;
			// background-color: red;

			// .scroll {
			// 	width: 100%;
			// 	height: 100%;
			
			
			

				.scroll_item {
					width: 100%;
					height: 120rpx;
					display: flex;
					align-items: center;
					padding-left: 40rpx;
					background-color: #fff;
					color: #fff;
					border-radius: 10rpx;
					margin-bottom: 20rpx;
					border-left: 10rpx solid #39CA35;

					.left {
						width: 90%;
						height: 100%;

						// background-color: pink;
						.top {
							width: 100%;
							height: 50%;
							font-size: 22rpx;
							display: flex;
							align-items: center;

							// background-color: yellow;
							.type {
								margin-left: 10rpx;
								margin-right: 20rpx;
								padding: 8rpx 15rpx;
								text-align: center;
								// line-height: 40rpx;
								border-radius: 10rpx;
								background-color: #1875D2;
								font-size: 16rpx;
								display: flex;
								align-items: center;
							}

							.state {
								color: #BABABA;
							}

						}

						.bottom {
							height: 50%;
							color: #000000;
							font-size: 26rpx;
							// background-color: pink;
							display: flex;
							align-items: center;
						}

					}

					.right {
						width: 10%;
						text-align: center;
						color: #000000;

						i {
							font-size: 22rpx;
						}
					}
				}
			// }
			
			
			
			.empty{
				width: 100%;
				height: 200rpx;
				display: flex;
				justify-content: center;
				align-items: center;
				font-size: 26rpx;
				// background-color: pink;
			}
		}
		
		
		
	}
</style>
