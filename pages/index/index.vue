<template>
	<view class="content">
		<view class="header">
			<view class="left">
				<i class="iconfont icon-a-svg5"></i>
			</view>
			<view class="title">智慧学工</view>
		</view>

		<view class="main">
			<view class="notice">
				<i class="iconfont icon-laba"></i>
				<text>如何入校申请，戳这里！</text>
			</view>

			<view class="main_left">
				<view class="main_item" @tap="toVacate">
					<view class="title">请假</view>
					<view class="icon">
						<i class="iconfont icon-a-svg2 first"></i>
					</view>
				</view>

				<view class="main_item small_item message">
					<view class="title">信息收集</view>
					<view class="icon">
						<i class="iconfont icon-text-box-multiple"></i>
					</view>
				</view>

				<view class="main_item small_item qiandao">
					<view class="title">签到</view>
					<view class="icon">
						<i class="iconfont icon-a-svg4"></i>
					</view>
				</view>

				<view class="main_item long_item jiancha">
					<view class="title">寝室检查</view>
					<view class="icon">
						<i class="iconfont icon-a-svg10"></i>
					</view>
				</view>

			</view>

			<view class="main_right">
				<view class="main_item long_item tongzhi">
					<view class="title">通知</view>
					<view class="icon">
						<i class="iconfont icon-a-svg1"></i>
					</view>
				</view>

				<view class="main_item small_item shenqing">
					<view class="title">申请</view>
					<view class="icon">
						<i class="iconfont icon-a-svg6"></i>
					</view>
				</view>

				<view class="main_item small_item huodon">
					<view class="title">活动报名</view>
					<view class="icon">
						<i class="iconfont icon-send-check"></i>
					</view>
				</view>


				<view class="main_item small_item liucheng">
					<view class="title">日常流程</view>
					<view class="icon">
						<i class="iconfont icon-swap-vertical-variant"></i>
					</view>
				</view>

				<view class="main_item small_item fanxiao">
					<view class="title">返校离校流程</view>
					<view class="icon">
						<i class="iconfont icon-a-svg11"></i>
					</view>
				</view>
				<view class="main_item long_item news">
					<view class="title">新闻公告</view>
					<view class="icon">
						<i class="iconfont icon-laba"></i>
					</view>

				</view>
			</view>
		</view>
		
		<view class="messageList">
			<view class="title">未读消息</view>
			<view class="tips">暂无未读消息</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			}
		},
		onLoad() {

		},
		methods: {
			toVacate(){
				uni.navigateTo({
					url:"../Vacate/Vacate"
				})
			}
		}
	}
</script>

<style lang="less">
	.content {
		padding-top: 70rpx;

		.header {
			height: 70rpx;
			padding: 10rpx;
			padding-left: 40rpx;
			display: flex;
			align-items: center;
			background-color: #EEEEEE;

			.left {
				height: 100%;
				padding-top: 10rpx;
				display: flex;
				align-items: center;
				justify-content: flex-end;
				font-size: 20rpx;
				margin-right: 40rpx;
			}

			.title {
				font-weight: 600;
			}
		}

		.main {
			padding: 20rpx;
			display: flex;
			justify-content: space-between;
			flex-wrap: wrap;
			background-color: #EEEEEE;

			.main_item {
				width: 100%;
				height: 350rpx;
				display: flex;
				flex-wrap: wrap;
				color: #fff;
				border-radius: 10rpx;
				margin-bottom: 20rpx;
				padding: 15rpx;
				background-color: #EF6191;

				.title {
					width: 100%;
					height: 50%;
					font-size: 24rpx;

				}

				.icon {
					width: 100%;
					height: 50%;
					display: flex;
					justify-content: flex-end;
					align-items: flex-end;

					i {}

					.first {
						font-size: 62rpx;
						padding: 15rpx;
					}
				}
			}

			.small_item {
				width: calc((100% - 20rpx) / 2);
				height: calc((350rpx - 20rpx) / 2);
			}

			.long_item {
				height: calc((350rpx - 20rpx) / 2);
			}

			.message {
				background-color: #01ACC2;
			}

			.qiandao {
				background-color: #26A59A;
			}

			.jiancha {
				background-color: #A0887E;
			}

			.tongzhi {
				background-color: #B968C7;
			}

			.shenqing {
				background-color: #9675CE;
			}

			.huodon {
				background-color: #7986CC;
			}
			
			.liucheng{
				background-color: #9CCC66;
			}
			
			.fanxiao{
				background-color: #FFA827;
			}
			
			.news{
				background-color: #FF8B66;
			}

			.notice {
				display: flex;
				width: 100%;
				align-items: center;
				padding: 25rpx 40rpx;
				color: #fff;
				border-radius: 10rpx;
				background-color: #FF8B66;
				margin-bottom: 20rpx;

				i {
					font-size: 36rpx;
					margin-right: 60rpx;
				}

				text {
					font-size: 24rpx;
				}
			}

			.main_left {
				width: calc((100% - 20rpx) / 2);
				display: flex;
				justify-content: space-between;
				flex-wrap: wrap;

			}

			.main_right {
				width: calc((100% - 20rpx) / 2);
				display: flex;
				justify-content: space-between;
				flex-wrap: wrap;

			}
		}
		
		
		.messageList{
			// padding: 20rpx;
			padding-left: 40rpx;
			padding-right: 40rpx;
			background-color: #EEEEEE;
			.title{
				font-size: 26rpx;
				font-weight: bold;
			}
			
			.tips{
				width: 100%;
				text-align: center;
				padding-top: 60rpx;
				font-size: 24rpx;
				color: #BABABA;
				
			}
		}
	}
</style>
