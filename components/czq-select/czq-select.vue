<template>
	<view class="only-select-mode">
		<view class="only-input">
			<input class="input-model" type="text" readonly="inputValue" @focus="focus" v-model="inputValue" :placeholder="placeholder" />
			<image v-if="clear" src="../../static/cancel.png" class="cancel" @click="clerCancel()"></image>
		</view>
		<view class="only-select" :class="{'open-tree': visible}">
			<view class="select-top" @click="cancel()"></view>
			<view class="select-bottom">
				<view class="czq-top" v-if="visible">
					<text class="text" @click="cancel()">返回</text>
					<text class="text" @click="confirm()">确定</text>
				</view>
				<view class="czq-content">
					<template v-if="onOff">
						<view class="czq-data" @click="mUserClick(item.id)" v-for="(item,index) in czqData" :key="index" :class="{'active-data' : (item.active ? true : false)}">
							<view class="pitc-on"></view>
							<text class="name">{{item.name}}</text>
							<view class="pitc-on">
								<text class="orhon-smart-icons">&#xe654;</text>
							</view>
						</view>
					</template>
					<template v-else>
						<view class="czq-data" @click="userClick(item)" v-for="(item,index) in czqData" :key="index" :class="{'active-data' : (userId === item.id ? true : false)}">
							<view class="pitc-on"></view>
							<text class="name">{{item.name}}</text>
							<view class="pitc-on">
								<text class="orhon-smart-icons">&#xe654;</text>
							</view>
						</view>
					</template>
				</view>
				<view v-if="czqData.length === 0 && visible" style="height:100%;">
					<u-empty text="数据为空" mode="data"></u-empty>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name:"czq-select",
		props:{
			cData: {
				type: Array,
				default:[
					{
						id: 0,
						name: '暂无数据'
					}
				]
			},
			multiple: {
				type: Boolean,
				default: false
			},
			placeholder: {
				type: String,
				default: '请选择'
			},
			cValue: {
				type: [String,Number],
				default: ''
			},
			clearble: {
				type: Boolean,
				default: false
			}
		},
		watch:{
			cData:{
				immediate: true,
				handler(value) {
					if(value.length > 0) {
						this.czqData = value.map(item => {
							return {
								id: item.id,
								name: item.name,
								active: false
							}
						});
					} else {
						this.czqData = [];
					}
				}
			},
			multiple: {
				immediate: true,
				handler(val) {
					this.onOff = val;
				}
			},
			clearble: {
				immediate: true,
				handler(val) {
					this.clear = val;
				}
			},
			cValue: {
				immediate: true,
				deep:true,
				handler(val) {
					// console.log('11选项默认值:', val);
					if(val) {
						this.inputValue = val;
					}
				}
			},
			// cValue(val) {
			// 	console.log('11选项默认值:', val);
			// 	if(val) {
			// 		this.inputValue = val;
			// 	} else {
			// 		console.log('选项默认值:', val);
			// 	}
			// }
		},
		computed:{
			
		},
		data() {
			return {
				czqData: [],
				inputValue: '',
				visible: false,
				userId: '',
				userName: '',
				onOff: false,
				clear: false
			};
		},
		methods: {
			focus(e) {
				uni.hideKeyboard();
				this.open();
			},
			confirm() {
				if(this.onOff) {
					var id = [];
					var name = [];
					for (var i = 0; i < this.czqData.length; i++) {
						if(this.czqData[i].active){
							id.push(this.czqData[i].id);
							name.push(this.czqData[i].name);
						}
					}
					this.inputValue = name.toString();
					this.$emit('input', id)
					this.visible = false;
				} else {
					this.$emit('input', this.userId)
					this.$emit('onlySelect', this.userId)
					this.inputValue = this.userName;
					this.visible = false;
				}
			},
			cancel() {
				this.visible = false;
			},
			open() {
				this.visible = true;
			},
			// 点击用户
			userClick(item) {
				this.userId = item.id;
				this.userName = item.name;
			},
			// 多选点击事件
			mUserClick(id) {
				let i = this.czqData.length;
				while(i--) {
					if(this.czqData[i].id === id) {
						this.czqData[i].active = !this.czqData[i].active;
					}
				}
			},
			// 清空
			clerCancel() {
				this.userClick({id: '',name: ''});
				this.$emit('input', null)
				this.inputValue = '';
				this.visible = false;
			}
		},
		created() {
			
		},
		mounted() {
			
		}
	}
</script>

<style lang="scss" scoped>
	.only-select-mode{
		height: 100%;
		
		.only-input{
			// height: inherit;
			display: flex;
			align-items: center;
			
			.input-model{
				height: 30px;
				text-indent: 0.5em;
				border: 1px solid #e0e0e0;
				border-radius: 4px;
				font-size: 14px;
				display: inherit;
				flex: 1;
			}
			.cancel{
				width: 25px;
				height: 25px;
			}
		}
	}
	.uni-searchbar{
		padding: 8px 0;
	}
	.only-select{
		height: 0px;
		display: flex;
		flex-direction: column;
		background-color: #000000ab;
		font-size: 13px;
		z-index: 1000;
		position: fixed;
		left: 0;
		right: 0;
		bottom: 0;
		transition-property: all;
		transition-duration: .3s;
		transition-timing-function: ease;
		transition-delay: 0s;
	}
	.orhon-smart-icons{
		font-size: 14px;
		display: none;
	}
	.active-data{
		color: #2979ff;
		background-color: #f0f8ff;
		.orhon-smart-icons{
			display: inline;
		}
	}
	.open-tree{
		height: 100%;
	}
	.select-top{
		flex: 1;
	}
	.select-bottom{
		height: 50%;
		background-color: white;
		border-top-left-radius: 12px;
		border-top-right-radius: 12px;
		padding: 10px 0;
		display: flex;
		flex-direction: column;
		flex-wrap: nowrap;
		
		.czq-top{
			border-bottom: 1px solid #ececec;
			display: flex;
			align-items: center;
			justify-content: space-between;
			min-height: 40px;
			// margin: 8px;
			// height: 36px;
			// padding: 8px 0;
			.text{
				width: 140rpx;
				height: 60rpx;
				text-align: center;
				line-height: 60rpx;
				border: 1px solid #d6d6d669;
				border-radius: 60rpx;
				margin-bottom: 10rpx;
				margin-left: 20rpx;
				margin-right: 20rpx;
			}
		}
		.czq-content{
			overflow-y: auto;
			flex: 1;
			// padding: 0 8px;
			
			.czq-data{
				// padding: 10px 15px 10px 5px;
				border-bottom: 1px solid #ffffff;
				// margin-left: 36px;
				display: flex;
				align-items: center;
				justify-content: center;
				// width: 65%;
				// padding: 10px 18px;
				height: 80rpx;
				border-radius: 3px;
				.name{
					flex: 1;
					text-align: center;
				}
				.pitc-on{
					width: 84rpx;
				}
				.orhon-smart-icons{
					font-size: 12px;
				}
			}
		}
		.select-search{
			border-bottom: 1px solid #ececec;
		}
		.select-content{
			flex: 1;
			display: flex;
			overflow: hidden;
			color: #353535;
			.content-left{
				width: 40%;
				display: flex;
				flex-direction: column;
				overflow: auto;
				flex-wrap: nowrap;
				.text-data{
					display: flex;
					align-items: center;
					padding: 10px 5px;
					border-top: 1px solid whitesmoke;
					justify-content: space-between;
					.orhon-smart-icons{
						font-size: 14px;
					}
				}
			}
			.content-right{
				background-color: whitesmoke;
				width: 60%;
				overflow: auto;
				display: flex;
				align-items: center;
				flex-direction: column;
				flex-wrap: nowrap;
			}
		}
		.select-button{
			display: flex;
			align-items: center;
			justify-content: space-around;
			border-top: 1px solid #eaeaea;
			padding-top: 8px;
			.cancel-class{
				border-color: #d6d6d6;
			}
		}
	}
</style>
