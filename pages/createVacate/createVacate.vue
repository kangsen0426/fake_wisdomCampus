<template>
	<view class="content">
		<view class="header">
			<view class="left" @tap="goBack">
				<i class="iconfont icon-jiantou-copy"></i>
			</view>
			<view class="title">我要请假</view>
		</view>

		<view class="main">

			<view class="form_item first_item">
				<view class="left_text">
					<span class="dot">*</span>
					<span class="text">请假类型</span>
				</view>
				<view class="inp">
					<!-- <input type="text" disabled v-model="vacateType" @tap="firstTapInp"></input> -->

					<picker :class="['piker',noPass1 ? 'noPass' : '']" @tap="firstTapInp" @cancel="cancel"
						@change="bindPickerChange" :value="index" :range="array">
						<view class="uni-input">{{array[index]}}</view>
						<view class="icons">
							<i v-if="noPass1" class="iconfont icon-jinggao error"></i>
							<i :class="['iconfont','icon-sanjiaoxing','arrow',vacateTypeTap ? 'rotate' : '']"></i>
						</view>
					</picker>
					<view v-if="noPass1" class="tips">请填选择请假类型</view>

				</view>
				<!-- <view class="icons">
					<i v-if="noPass1" class="iconfont icon-jinggao error"></i>
					<i :class="['iconfont','icon-sanjiaoxing',vacateTypeTap ? 'rotate' : '']"></i>
				</view> -->
			</view>


			<view class="form_item">
				<view class="left_text">
					<span class="dot">*</span>
					<span class="text">开始时间</span>
				</view>
				<view class="inp">
					<view :class="['piker',noPass2 ? 'noPass' : '']">
						<view class="uni-input">{{date}} {{time}}</view>
						<view class="icons">
							<i class="iconfont icon-a-svg3">
								<picker class="innerPiker" mode="date" :value="date" :start="startDate" :end="endDate"
									@change="bindDateChange" @cancel="cancelDate">
								</picker>
							</i>
							<i class="iconfont icon-a-svg2">
								<picker class="innerPiker" @cancel="cancelTime" mode="time" :value="time" start="00:00"
									end="23:59" @change="bindTimeChange">
								</picker>
							</i>
							<i v-if="noPass2" class="iconfont icon-jinggao error"></i>
						</view>
					</view>
					<view v-if="noPass2" class="tips">请填选择开始时间</view>

				</view>

			</view>


			<view class="form_item">
				<view class="left_text">
					<span class="dot">*</span>
					<span class="text">结束时间</span>
				</view>
				<view class="inp">
					<view :class="['piker',noPass3 ? 'noPass' : '']">
						<view class="uni-input">{{date2}} {{time2}}</view>
						<view class="icons">
							<i class="iconfont icon-a-svg3">
								<picker class="innerPiker" mode="date" :value="date2" :start="startDate" :end="endDate"
									@change="bindDateChange2" @cancel="cancelDate2">
								</picker>
							</i>
							<i class="iconfont icon-a-svg2">
								<picker class="innerPiker" @cancel="cancelTime" mode="time" :value="time2" start="00:00"
									end="23:59" @change="bindTimeChange2">
								</picker>
							</i>
							<i v-if="noPass3" class="iconfont icon-jinggao error"></i>
						</view>
					</view>
					<view v-if="noPass3" class="tips">请填选择结束时间</view>

				</view>

			</view>


			<view class="form_item">
				<view class="left_text">
					<span class="dot">*</span>
					<span class="text">需要离校</span>
				</view>
				<view class="inp">

					<div class="switchBtn">
						<view :class="['switchBox',switch1Move ? 'switchBoxChange' : '']" @tap="switch1Change">
							<view :class="['cicle',switch1Move ? 'cicleMove' : '']"></view>
						</view>
					</div>

				</view>

			</view>


			<view class="form_item">
				<view class="left_text">
					<span class="dot">*</span>
					<span class="text">需要出省</span>
				</view>
				<view class="inp">

					<div class="switchBtn">
						<view :class="['switchBox',switch2Move ? 'switchBoxChange' : '']" @tap="switch2Change">
							<view :class="['cicle',switch2Move ? 'cicleMove' : '']"></view>
						</view>
					</div>

				</view>

			</view>

			<view class="form_item">
				<view class="left_text">
					<span class="dot">*</span>
					<span class="text">需要出市</span>
				</view>
				<view class="inp">

					<div class="switchBtn">
						<view :class="['switchBox',switch3Move ? 'switchBoxChange' : '']" @tap="switch3Change">
							<view :class="['cicle',switch3Move ? 'cicleMove' : '']"></view>
						</view>
					</div>

				</view>

			</view>


			<view class="form_item lastItem">
				<view class="left_text">
					<span class="dot">*</span>
					<span class="text">请假原因</span>
				</view>
				<view class="inp">

					<div class="textAreaBox">
						<textarea :class="[noPassText ? 'noPassText' : '',textareaActive ? 'textareaActive' : '']"
							@focus="textareaFocus" :value="textArea" @blur="bindTextAreaBlur" />
						<i v-if="noPassText" class="iconfont icon-jinggao areaError"></i>
					</div>
					<view v-if="noPassText" class="tips">请填写请假原因</view>
				</view>

			</view>


			<view class="form_item contactBox">
				<view class="left_text">
					<span class="dot"></span>
					<span class="text longText">紧急联系人</span>
				</view>
				<view class="inp">
					<input :class="['contact',contactActive ? 'contactActive' : '']" type="number" v-model="contact"
						@focus="contactFocus" @blur="contactBlur" />
				</view>

			</view>

			<view class="imgUperLoad_wrap">
				<view class="head">
					<view class="title">添加附件</view>
					<view class="tips">图片格式支持：jpg、png、jpeg</view>
				</view>

				<view class="imageUperLoad">
					<view class="title">
						<span>图片上传(每张5M以内)</span>
						<span @tap="chooseImage">
							<i class="iconfont icon-checkbox-plus-full"></i>
						</span>
					</view>
					<!-- <view class="imgBox"> -->
					<scroll-view scroll-y class="imgBox">
						<view class="img_item" v-for="(item,index) in tempFilePaths" :v-key="item">
							<image mode="aspectFill" :src="item.path">
							</image>
							<view class="mask">
								<view class="message">
									<view class="name">{{item.name}}</view>
									<view class="process">{{(item.size / (1024*1024)).toFixed(2)}}M / 100.00%</view>
								</view>
								<view class="icon">
									<i class="iconfont icon-gou"></i>
								</view>
							</view>

						</view>





					</scroll-view>

					<!-- </view> -->
				</view>
			</view>


			<view class="positionItem">
				<view class="left_text">
					<span class="dot"></span>
					<span class="text">定位</span>
				</view>
				<view class="inp">

					<view class="inner">
						<input type="text" disabled :value="positionText" />
						<view class="btn" @tap="resetPosition">重新定位</view>
					</view>

				</view>

			</view>


			<view class="bottom_wrap">
				<view class="left" @tap="goBack">取消</view>
				<view class="right" @tap="submitVacate">提交请假</view>
			</view>



		</view>
	</view>
</template>

<script>
	export default {
		data() {
			const currentDate1 = ''
			const currentDate2 = ''
			return {
				array: ['', '事假', '病假', '晚自习请假', "晨读请假"],
				index: 0,
				date: currentDate1,
				time: '',
				date2: currentDate2,
				time2: '',
				textArea: '',
				contact: '',
				positionText: '',
				vacateType: '事假',
				vacateTypeTap: false,
				noPass1: false,
				noPass2: false,
				noPass3: false,
				noPassText: false,
				switch1Move: false,
				switch2Move: false,
				switch3Move: false,
				contactActive: false,
				textareaActive: false,
				tempFilePaths: [],
				savedFilePathArr: []
			};
		},
		computed: {
			startDate() {
				return this.getDate('start');
			},
			endDate() {
				return this.getDate('end');
			}
		},
		onShow() {

			// uni.getLocation({
			// 	type: 'gcj02',
			// 	geocode:true,
			// 	success: function(res) {
			// 		console.log('当前位置的经度：' + res.longitude);
			// 		console.log('当前位置的纬度：' + res.latitude);
			// 		console.log('位置信息: ' + res.address);
			// 		console.log(res.address.province);
			// 		console.log(res.address.city);
			// 		console.log(res.address.district);
			// 		console.log(res.address.street);
			// 		console.log(res.address.streetNum);
			// 		console.log(res.address.poiName);
			// 	}
			// })

		},
		methods: {
			
			tody(){
				
				let date = new Date()
								
				let day = date.getDate();
				let month = date.getMonth() + 1
				
				return `${month}-${day} 14:30`
				
			},
			
			sliceTime(timeStr) {

				let index = timeStr.indexOf('-')
				let newStr = timeStr.slice(index + 1, timeStr.length)

				
				return newStr

			},
			timeDifference(start, end) {

				console.log(start.replace(/-/g, "/"));
				console.log(end.replace(/-/g, "/"));

				let dateBegin = new Date(start.replace(/-/g, "/")); //转化为Date对象的形式
				let dateEnd = new Date(end.replace(/-/g, "/"));


				let dateDiff = dateEnd.getTime() - dateBegin.getTime(); //时间差的毫秒数
				let dayDiff = Math.floor(dateDiff / (24 * 3600 * 1000)); //计算出相差天数
				let leave1 = dateDiff % (24 * 3600 * 1000) //计算天数后剩余的毫秒数
				let hours = Math.floor(leave1 / (3600 * 1000)) //计算出小时数


				if (dayDiff === 0) {
					return `${hours}小时`
				} else {
					return `${dayDiff}天${hours}小时`
				}
			},
			saveImage() {
				let self = this

				for (let i = 0; i < this.tempFilePaths.length; i++) {

					uni.saveFile({
						tempFilePath: this.tempFilePaths[i].path,
						success: (res) => {



							self.savedFilePathArr.push(res.savedFilePath)

							console.log(self.savedFilePathArr)
						},
						fail: (err) => {

							uni.showToast({
								icon: "error",
								title: "图片保存错误请重试"
							})
						}
					})

				}
			},
			submitVacate() {

				//逐一验证表单数据

				if (this.index === 0) {
					this.noPass1 = true

					return
				}

				if (this.time === '') {
					this.noPass2 = true

					return
				}


				if (this.time2 === '') {
					this.noPass3 = true

					return
				}

				if (this.textArea === '') {
					this.noPassText = true

					return
				}

				if (this.positionText === '') {

					uni.showToast({
						icon: "error",
						title: "请选择定位"
					})

					return
				}

				//如果有图片，先保存在本地
				if (this.tempFilePaths.length !== 0) {

					this.saveImage()

				}

				uni.showLoading()


				//收集数据
				let startTime = this.date + " " + this.time
				let endTime = this.date2 + " " + this.time2

				setTimeout(() => {

					let dataParams = {
						vacateType: this.array[this.index], //请假类型
						startTime, //开始结束时间
						endTime,
						leaveSchool: this.switch1Move, //是否离校等
						leaveprovinces: this.switch2Move,
						leaveCity: this.switch3Move,
						vacateResone: this.textArea,
						concatPhone: this.contact,
						savedFilePathArr: this.savedFilePathArr,
						position: this.positionText,
						timeDifference: this.timeDifference(startTime, endTime),
						sliceTime1:this.sliceTime(startTime),
						sliceTime2:this.sliceTime(endTime),
						passDay:this.tody()
					}


					console.log(dataParams)

					//读取原来的数据
					let vacateData = uni.getStorageSync('vacateData') || []

					//更新数据
					vacateData.unshift(dataParams)

					//保存数据
					uni.setStorageSync('vacateData', vacateData)

					//跳转页面

					console.log(vacateData)

					uni.hideLoading()
					
					uni.navigateTo({
						url:`../vacateDetail/vacateDetail`,
						success() {
							uni.$emit('vacateDetail',dataParams)
						}
					})

				}, 300)





			},
			resetPosition() {

				let self = this

				uni.chooseLocation({
					success: function(res) {
						console.log('位置名称：' + res.name);
						console.log('详细地址：' + res.address);
						console.log('纬度：' + res.latitude);
						console.log('经度：' + res.longitude);

						self.positionText = res.address
					}
				});
			},
			chooseImage() {

				let self = this
				uni.chooseImage({

					sourceType: ['album', 'camera'],
					success: function(res) {

						console.log(res)

						for (let i = 0; i < res.tempFiles.length; i++) {
							self.tempFilePaths.push(res.tempFiles[i])
						}


						console.log(self.tempFilePaths)

					}
				});
			},
			bindTextAreaBlur: function(e) {
				this.textareaActive = false
				if (e.detail.value === '') {
					this.noPassText = true
				} else {
					this.noPassText = false
				}
				this.textArea = e.detail.value
			},
			textareaFocus() {
				this.textareaActive = true
			},
			contactFocus() {
				this.contactActive = true
			},
			contactBlur() {
				this.contactActive = false
			},
			switch1Change() {
				this.switch1Move = !this.switch1Move
			},
			switch2Change() {
				if (!this.switch2Move && !this.switch1Move) {
					this.switch1Move = true
				}
				this.switch2Move = !this.switch2Move
			},
			switch3Change() {
				if (!this.switch3Move && !this.switch1Move) {
					this.switch1Move = true
				}
				if (!this.switch3Move && !this.switch2Move) {
					this.switch2Move = true
				}
				this.switch3Move = !this.switch3Move
			},
			bindPickerChange: function(e) {
				this.vacateTypeTap = false
				console.log('picker发送选择改变，携带值为', e.target.value)
				this.index = e.target.value

				if (this.index === 0) {
					this.noPass1 = true
				} else {
					this.noPass1 = false
				}
			},
			bindDateChange: function(e) {
				this.date = e.target.value
				if (this.time === '') {
					this.time = "00:00"
				}

				if (this.date === '') {
					this.noPass2 = true
				} else {
					this.noPass2 = false
				}
			},
			bindDateChange2: function(e) {
				this.date2 = e.target.value
				if (this.time2 === '') {
					this.time2 = "00:00"
				}

				if (this.date2 === '') {
					this.noPass3 = true
				} else {
					this.noPass3 = false
				}
			},
			bindTimeChange: function(e) {
				if (this.date === '') {
					const date = new Date();
					let year = date.getFullYear();
					let month = date.getMonth() + 1;
					let day = date.getDate();

					month = month > 9 ? month : '0' + month;
					day = day > 9 ? day : '0' + day;
					this.date = `${year}-${month}-${day}`;

					this.time = e.target.value
					this.noPass2 = false
				} else {
					this.time = e.target.value
				}
			},
			bindTimeChange2: function(e) {
				if (this.date2 === '') {
					const date = new Date();
					let year = date.getFullYear();
					let month = date.getMonth() + 1;
					let day = date.getDate();

					month = month > 9 ? month : '0' + month;
					day = day > 9 ? day : '0' + day;
					this.date2 = `${year}-${month}-${day}`;

					this.time2 = e.target.value
					this.noPass3 = false
				} else {
					this.time2 = e.target.value
				}
			},
			cancel() {
				if (this.index === 0) {
					this.noPass1 = true
				} else {
					this.noPass1 = false
				}
			},
			cancelDate() {
				if (this.date === '') {
					this.noPass2 = true
				} else {
					this.noPass2 = false
				}
			},
			cancelDate2() {
				if (this.date2 === '') {
					this.noPass3 = true
				} else {
					this.noPass3 = false
				}
			},
			cancelTime() {
				if (this.date === '') {

				} else {
					if (this.time === '') {
						this.time = '00:00'
					} else {

					}
				}
			},
			cancelTime2() {
				if (this.date2 === '') {

				} else {
					if (this.time2 === '') {
						this.time2 = '00:00'
					} else {

					}
				}
			},
			goBack() {
				uni.navigateBack({
					delta: 1
				})
			},
			firstTapInp() {
				console.log("focus")

				this.vacateTypeTap = true

			},
			getDate(type) {
				const date = new Date();
				let year = date.getFullYear();
				let month = date.getMonth() + 1;
				let day = date.getDate();

				if (type === 'start') {
					year = year - 2;
				} else if (type === 'end') {
					year = year + 2;
				}
				month = month > 9 ? month : '0' + month;
				day = day > 9 ? day : '0' + day;
				return `${year}-${month}-${day}`;
			}
		}
	}
</script>

<style lang="less">
	.content {
		padding-top: 90rpx;
		padding-bottom: 100rpx;

		.header {
			// height: 70rpx;
			// padding: 10rpx;
			// padding-left: 40rpx;
			// display: flex;
			// align-items: center;
			// background-color: #EEEEEE;
			// background-color: pink;

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
			padding-top: 90rpx;
			background-color: #EEEEEE;

			.first_item {
				border-top-left-radius: 20rpx;
				border-top-right-radius: 20rpx;
			}

			.contactBox {
				margin-top: 20rpx;
				border-top-left-radius: 20rpx;
				border-top-right-radius: 20rpx;
			}

			.lastItem {
				border-bottom-left-radius: 20rpx;
				border-bottom-right-radius: 20rpx;
			}

			.positionItem {
				margin-top: 20rpx;
				border-radius: 20rpx;
				display: flex;
				align-items: center;
				padding: 20rpx 30rpx;
				background-color: #fff;
				font-size: 26rpx;

				.left_text {
					width: 12%;
					padding-right: 30rpx;
				}

				.inp {
					width: 88%;
					height: 100%;
					// background-color: pink;

					.inner {
						padding: 20rpx 0;
						display: flex;
						align-items: center;

						input {
							width: 80%;
							font-size: 20rpx;


						}

						.btn {
							width: 20%;
							color: #1875D2;
							// background-color: yellow;
						}
					}

				}
			}

			.form_item {
				display: flex;
				align-items: center;
				padding: 20rpx 30rpx;
				background-color: #fff;
				// position: relative;
				border-bottom: 1rpx solid #dcdcdc;

				.left_text {
					display: flex;
					align-items: center;
					// width: 25%;
					padding-right: 30rpx;
					// background-color: pink;

					.dot {
						// display: block;
						// box-sizing: content-box;
						color: red;
						margin-top: 10rpx;
						margin-right: 6rpx;

					}

					.text {

						font-size: 26rpx;
					}

					.longText {
						font-size: 22rpx;
					}

				}

				.inp {
					width: 76%;
					display: flex;
					flex-wrap: wrap;
					// background-color: pink;
					// input {
					// 	width: 100%;
					// 	height: 80rpx;
					// 	border-radius: 10rpx;
					// 	padding: 0 20rpx;
					// 	font-size: 26rpx;
					// 	border: 3rpx solid #dadada;
					// 	// border: 5rpx solid #1875D2;



					// 	.active {
					// 		border: 6rpx solid #1875D2;
					// 	}


					// }



					.contact {
						width: 100%;
						height: 80rpx;
						padding: 0 20rpx;
						border-radius: 10rpx;
						border: 3rpx solid #dadada;
						transition: all 0.3s;
						// background-color: pink;


					}

					.contactActive {
						border: 5rpx solid #1875D2;
					}

					.switchBtn {
						width: 100%;
						padding: 15rpx 0;
						display: flex;
						justify-content: flex-end;

						// background-color: pink;

						.switchBox {
							width: 75rpx;
							height: 35rpx;
							border-radius: 50rpx;
							position: relative;
							background-color: #C9C9C9;
							transition: all 0.5s;

							.cicle {
								position: absolute;
								left: 0;
								top: -10rpx;
								width: 50rpx;
								height: 50rpx;
								border-radius: 50%;
								background-color: #fff;
								box-shadow: 0rpx 1rpx 5rpx #868686;
								transition: all 0.5s;
							}

							.cicleMove {
								left: 30rpx;
								background-color: #1976D3;
							}
						}

						.switchBoxChange {
							background-color: #86B5E5;
						}
					}

					.piker {
						width: 100%;
						height: 75rpx;
						border-radius: 10rpx;
						padding: 20rpx 20rpx;
						font-size: 26rpx;
						border: 3rpx solid #dadada;
						position: relative;
						display: flex;
						// display: flex;
						// align-items: center;
						// justify-content: space-between;
						// flex-wrap: wrap;
						// border: 5rpx solid #1875D2;




						.active {
							border: 5rpx solid #1875D2;
						}


						.icons {
							position: absolute;
							right: 40rpx;
							top: 20rpx;
							// float: right;
							display: flex;

							i {
								font-size: 32rpx;
								color: #797979;
								margin-left: 20rpx;
								transition: all 0.2s;
								position: relative;

								.innerPiker {
									position: absolute;
									top: 0;
									width: 100%;
									height: 100%;
									// background-color: red;
								}
							}

							.arrow {
								font-size: 20rpx;
							}

							.error {
								color: #BF0118;
							}

							// .rotate {
							// 	display: block;
							// 	transform: rotate(180deg);
							// }

						}

					}

					.tips {
						color: #BF0118;
						margin-left: 40rpx;
						font-size: 16rpx;
						padding-top: 10rpx;
					}

					.noPass {
						border: 5rpx solid #BF0118;
					}

					.textAreaBox {
						width: 100%;
						position: relative;

						textarea {
							width: 100%;
							height: 200rpx;
							border: 3rpx solid #dadada;
							border-radius: 10rpx;
							padding: 15rpx;
							font-size: 26rpx;
							transition: all 0.5s;
							// background-color: pink;


						}

						.textareaActive {
							border: 5rpx solid #1875D2;
						}

						.noPassText {
							border: 5rpx solid #BF0118;
						}

						.areaError {
							position: absolute;
							right: 20rpx;
							top: 20rpx;

							color: #BF0118;
						}
					}
				}



				// .icons {
				// 	position: absolute;
				// 	right: 70rpx;

				// 	i {
				// 		font-size: 20rpx;
				// 		color: #797979;
				// 		transition: all 0.2s;
				// 	}

				// 	.error{
				// 		color: #BF0118;
				// 		margin-right: 20rpx;
				// 		font-size: 32rpx;
				// 	}

				// 	.rotate {
				// 		display: block;
				// 		transform: rotate(180deg);
				// 	}

				// }
			}


			.imgUperLoad_wrap {
				font-size: 26rpx;
				padding: 20rpx 30rpx;
				padding-bottom: 30rpx;
				border-bottom-left-radius: 20rpx;
				border-bottom-right-radius: 20rpx;
				background-color: #FFFFFF;

				.head {
					padding-bottom: 15rpx;

					.title {
						padding-left: 10rpx;
					}

					.tips {
						font-size: 20rpx;
						color: #bfbfbf;
					}
				}

				.imageUperLoad {
					min-height: 230rpx;
					border-radius: 10rpx;
					box-shadow: 0rpx 2rpx 7rpx #676767;

					// overflow: hidden;
					// background-color: pink;
					.title {
						height: 100rpx;
						border-top-left-radius: 10rpx;
						border-top-right-radius: 10rpx;
						padding: 0 20rpx;
						padding-right: 30rpx;
						background-color: #1875D2;
						color: #fff;
						display: flex;
						align-items: center;
						justify-content: space-between;
					}

					.imgBox {
						min-height: 130rpx;
						max-height: 500rpx;
						overflow: hidden;
						padding: 15rpx;

						// .scrollView{
						// 	height: 100%;
						// 	overflow-y: auto;
						.img_item {
							border-radius: 10rpx;
							// background-color: pink;
							margin-bottom: 15rpx;
							position: relative;

							image {
								width: 100%;
								height: 350rpx;
								border-radius: 10rpx;

							}

							.mask {
								position: absolute;
								top: 0;
								left: 0;
								right: 0;
								width: 100%;
								height: 100rpx;
								padding-left: 15rpx;
								display: flex;
								align-items: center;
								color: #fff;
								box-shadow: 0 17rpx 30rpx -5rpx #333333 inset;

								.message {
									width: 85%;

									// background-color: pink;

									.name {}

									.process {}
								}

								.icon {
									width: 15%;
									text-align: center;

									i {
										font-size: 36rpx;
									}
								}
							}


						}

						// }


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
					width: 40%;
					height: 100%;
					color: #BEBEBE;
					display: flex;
					align-items: center;
					justify-content: center;
					background-color: #fff;
				}

				.right {
					width: 60%;
					height: 100%;
					display: flex;
					align-items: center;
					justify-content: center;
					background-color: #1875D2;
					border-radius: 10rpx;
				}
			}


		}
	}
</style>
