<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<text class="title">{{title}}</text>
		</view>
		
		<czq-select :cData="cData" v-model="value1" placeholder="请选择" class="ccc"></czq-select>
		
		<uni-forms :value="formData" ref="form" validate-trigger="bind" err-show-type="undertext" labelPosition="left" class="leave-form">
			<uni-forms-item required name="studentList" label="学生" class="leave-item">
				<czq-select :cData="cData" :multiple="true" v-model="formData.studentList" placeholder="请选择学生"></czq-select>
			</uni-forms-item>
			
			<uni-forms-item name="leaveKind" required label="请假类型" class="leave-item">
				<czq-select :cData="cData" :multiple="false" v-model="formData.leaveKind" placeholder="请选择请假类型"></czq-select>
			</uni-forms-item>
			
			<uni-forms-item name="leaveClassify" required label="请假分类" class="leave-item">
				<czq-select :cData="cData" :multiple="false" v-model="formData.leaveClassify" placeholder="请选择请假分类"></czq-select>
			</uni-forms-item>
		</uni-forms>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				value1: 1,
				cData: [
					{
						id: 1,
						name: '九州'
					},
					{
						id: 2,
						name: '华夏'
					},
					{
						id: 3,
						name: '中华'
					},
					{
						id: 4,
						name: '神州'
					}
				],
				formData: {
					leaveKind: null,
					leaveClassify: null,
					studentList:undefined
				},
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style lang="scss" scoped>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		padding: 0 14px;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 60rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 30rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
	
	.leave-form{
		width: 100%;
	}
	.ccc{
		margin: 40rpx 0;
	}
</style>
