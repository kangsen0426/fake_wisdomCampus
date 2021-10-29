<template>
	<view class="content">
		<view class="header">
			<view class="left" @tap="backList">
				<i class="iconfont icon-jiantou-copy"></i>
			</view>
			<view class="title">请假信息</view>
		</view>

		<view class="main">

			<view class="first_item">
				<view class="item_header">
					<view class="pass">
						<i class="iconfont icon-gou gou"></i>
						<span>审批通过</span>
					</view>
					<!-- <view class="destruction">
						<span class="descText">已销假</span>
						<span>(10-25 22:12)</span>
					</view> -->
				</view>

				<view class="first_item_mesage">
					<view class="first_item_inner_message">
						<span>请假类型：</span>
						<span class="message_tips">{{Detaildata.vacateType}}</span>
					</view>
					<view class="first_item_inner_message">
						<span>需要离校：</span>
						<span
							:class="['message_tip',Detaildata.leaveSchool ?'special': '']">{{Detaildata.leaveSchool ? '是' : '否'}}</span>
					</view>
					<view class="first_item_inner_message">
						<span>需要出市：</span>
						<span
							:class="['message_tip',Detaildata.leaveprovinces ?'special': '']">{{Detaildata.leaveprovinces ? '是' : '否'}}</span>
					</view>
					<view class="first_item_inner_message">
						<span>需要出省：</span>
						<span
							:class="['message_tip',Detaildata.leaveCity ?'special': '']">{{Detaildata.leaveCity ? '是' : '否'}}</span>
					</view>
				</view>


			</view>

			<view class="second_item_message">
				<view class="message_title">
					<view>请假详情</view>
				</view>

				<view class="second_item_inner_message">
					<span>请假时间：</span>
					<span class="message_tips">{{Detaildata.timeDifference}}({{Detaildata.sliceTime1}} ~
						{{Detaildata.sliceTime2}})</span>
				</view>

				<view class="second_item_inner_message">
					<span>发起时间：</span>
					<span class="message_tips">{{Detaildata.startTime}}</span>
				</view>

				<view class="second_item_inner_message">
					<span>请假原因：</span>
					<span class="message_tips">{{Detaildata.vacateResone}}</span>
				</view>

				<view class="second_item_inner_message">
					<span>发起位置：</span>
					<span class="message_tips">{{Detaildata.position}}</span>
				</view>
			</view>


			<view class="three_item_message">
				<view class="message_title">
					<view>请假流程记录</view>
				</view>

				<view class="vacate_process">

					<view class="left_process">
						<view class="first_dot"></view>
						<view class="line_wrap">
							<view class="sec_line"></view>
						</view>
						<view class="last_dot"></view>
					</view>

					<view class="right_wrap">
						<view class="start_time">
							<span>{{Detaildata.startTime}}</span>
						</view>
						<view class="vacater">
							<span class="message_tips">晏绍杰 - 发起申请</span>
						</view>
						<view class="end_time">
							<span>{{Detaildata.passDay}}</span>
						</view>

						<view class="vacate_pass">
							<span class="message_tips">徐新宇 - 审批通过</span>
						</view>
					</view>
				</view>
			</view>
		</view>

		<view class="bottom_wrap">
			<view class="left">请假信息二维码</view>
			<view class="right">销假</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Detaildata: {}
			};
		},
		onLoad() {

			
			uni.$on('vacateDetail', (data) => {
				this.Detaildata = data
			
			})
			
			console.log(this.Detaildata)
			

		},
		methods: {
			backList() {
				uni.navigateTo({
					url: "../Vacate/Vacate"
				})
			}
		}
	}
</script>

<style lang="less">
	.content {
		padding-top: 90rpx;
		padding-bottom: 100rpx;
		background-color: #EEEEEE;

		.header {
			box-sizing: content-box;
			position: fixed;
			height: 70rpx;
			top: 0;
			left: 0;
			right: 0;
			z-index: 999;
			padding: 0rpx 40rpx;
			padding-top: 80rpx;
			display: flex;
			// justify-content: space-between;
			align-items: center;
			// z-index: 9999;
			background-color: #EEEEEE;
			// background-color: pink;


			.left {
				height: 100%;
				padding-top: 10rpx;
				display: flex;
				align-items: center;
				justify-content: flex-end;
				font-size: 20rpx;
				margin-right: 40rpx;

				i {
					font-weight: bold;
					font-size: 26rpx;
				}
			}

			.title {
				font-weight: 600;
			}
		}

		.main {

			padding-top: 70rpx;
			background-color: #EEEEEE;

			.first_item {
				border-bottom-left-radius: 10rpx;
				border-bottom-right-radius: 10rpx;
				background-color: #fff;
				overflow: hidden;

				.item_header {
					// height: 100rpx;
					display: flex;
					justify-content: center;
					align-items: center;
					flex-wrap: wrap;
					padding: 32rpx;
					border-top-left-radius: 10rpx;
					border-top-right-radius: 10rpx;
					font-size: 26rpx;
					color: #fff;
					background-color: #21BA45;

					.pass {

						.gou {
							font-size: 24rpx;
							margin-right: 5rpx;

						}
					}

					.destruction {
						width: 100%;
						text-align: center;

						.descText {
							font-size: 36rpx;
						}
					}

				}

				.first_item_mesage {
					padding: 30rpx;
					display: flex;
					flex-wrap: wrap;

					.first_item_inner_message {
						width: 50%;
						font-size: 0;
						// background-color: pink;

						span {
							font-size: 22rpx;
							color: #a8a8a8;
						}

						.message_tips {
							font-size: 24rpx;
							color: #000000;
						}

						.special {
							color: #f0ce45;
						}
					}
				}


			}




			.second_item_message {
				padding: 30rpx;
				display: flex;
				flex-wrap: wrap;
				margin-top: 20rpx;
				border-radius: 10rpx;
				background-color: #FFFFFF;

				.message_title {
					width: 100%;
					font-size: 24rpx;
					font-weight: bold;
					padding-bottom: 20rpx;


				}


				.second_item_inner_message {
					width: 100%;

					span {
						font-size: 22rpx;
						color: #a8a8a8;
					}

					.message_tips {
						font-size: 24rpx;
						color: #000000;
					}

				}
			}

			.three_item_message {
				padding: 30rpx;
				padding-bottom: 80rpx;
				display: flex;
				flex-wrap: wrap;
				margin-top: 20rpx;
				border-radius: 10rpx;
				background-color: #FFFFFF;

				.message_title {
					width: 100%;
					font-size: 24rpx;
					font-weight: bold;
					padding-bottom: 20rpx;


				}

				.vacate_process {
					padding: 10rpx;
					display: flex;
					flex-wrap: wrap;

					.left_process {
						width: 100rpx;
						height: 216rpx;
						padding-top: 8rpx;
						padding-left: 15rpx;
						display: flex;
						flex-wrap: wrap;
						justify-content: flex-start;

						.first_dot {
							width: 32rpx;
							height: 32rpx;
							border-radius: 50%;
							background-color: #9E9E9E;
						}

						.line_wrap {
							width: 100%;
							// padding: 5rpx 0;
							padding-left: 13rpx;

							.sec_line {
								width: 6rpx;
								height: 110rpx;
								background-color: #D8D8D8;
							}

						}


						.last_dot {
							width: 32rpx;
							height: 32rpx;
							border-radius: 50%;
							background-color: #21BA45;
						}
					}

					.right_wrap {
						font-size: 0;

						// background-color: pink;
						span {
							font-size: 23rpx;
							color: #a8a8a8;
						}

						.message_tips {
							font-size: 22rpx;
							color: #000000;
						}

						.start_time {
							padding-bottom: 38rpx;
						}

						.vacater {
							padding-bottom: 48rpx;
						}

						.end_time {
							padding-top: 15rpx;
						}

						.vacate_pass {
							padding-top: 38rpx;
						}
					}
				}
			}
		}


		.bottom_wrap {
			position: fixed;
			bottom: 0;
			left: 0;
			right: 0;
			height: 100rpx;
			display: flex;
			align-items: center;
			font-size: 28rpx;
			color: #fff;
			background-color: #fff;
			border-top: 1rpx solid #c8c8c8;

			.left {
				width: 60%;
				height: 100%;
				color: #1875D2;
				display: flex;
				align-items: center;
				justify-content: center;
				background-color: #fff;
			}

			.right {
				width: 40%;
				height: 100%;
				display: flex;
				align-items: center;
				justify-content: center;
				background-color: #1875D2;

				border-radius: 10rpx;
			}
		}

	}
</style>
