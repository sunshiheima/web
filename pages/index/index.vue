<template>
	<view class="content">

		<view class="shopchar">
			<view class="table">
				<view class="thead">
					<view class="shopchar-title">
						<text class="allchecked">
							<text>
								<checkbox value="cb" @click="allChecked(checkAll)" :checked="checkAll" class="allchecked-in" style="transform:scale(0.8)" />
							</text>
							全选
						</text>
						<text style="flex: 1;color: #333333;font-weight: bold;margin-left: 20rpx;">sunshiheima孙氏黑马官方旗舰店</text>
					</view>
				</view>
				<view class="tbody">
					<view class="tr" v-for="(val,idx) in list" :key="val.id">
						<view>
							<checkbox @click="checkedChang(val.id)" value="cb" :checked="val.bg" class="allchecked-in" style="transform:scale(0.8)" />
						</view>
						<view>
							<image :src="'../../static/imgs/'+val.url" mode=""></image>
						</view>
						<view class="goodsinof">
							<text class="good-title">{{val.name}}</text>
							<text class="goods-price">单价：<text class="goods-price-in">￥{{val.price}}</text></text>
							<text class="goods-old">原价：<text class="del-old">￥{{val.old}}</text></text>
						</view>
						<view class="buttons">
							<view class="btnbox">
								<button type="default" size="mini" @click="add(val.id)">+</button>
							</view>
							<text class="good-price">{{val.num}}</text>
							<view class="btnbox sub">
								<button type="default" size="mini" @click="sub(val.id)">-</button>
							</view>
						</view>
						<view class="delbox-out">
							<view class="delbox">
								<button type="default" size="mini" @click="del(val.id)">删除</button>

							</view>
						</view>
					</view>
				</view>
			</view >
			<view class="footall">
				<text class="footAll-price">总价：<text class="all-price">￥{{allPrice}}</text></text>
				<text class="close"><text>去结算</text></text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [{
						id: 1,
						name: '孙氏黑马眼镜',
						price: 38,
						old: 56,
						url: '1.jpg',
						bg: false,
						num: 1
					},
					{
						id: 2,
						name: '孙氏黑马眼镜',
						price: 45,
						old: 67,
						url: '2.jpg',
						bg: false,
						num: 1
					},
					{
						id: 3,
						name: '孙氏黑马眼镜',
						price: 33,
						old: 23,
						url: '3.jpg',
						bg: false,
						num: 1
					},
					{
						id: 4,
						name: '孙氏黑马眼镜',
						price: 2,
						old: 6,
						url: '4.png',
						bg: false,
						num: 1
					},
					{
						id: 5,
						name: '孙氏黑马眼镜',
						price: 77,
						old: 99,
						url: '5.jpg',
						bg: false,
						num: 1
					},
				],
				checkAll: false,
			}
		},
		onLoad() {

		},
		methods: {
			checkedChang(id) {
				// console.log('0000')
				for (let val of this.list) {
					if (val.id === id) {
						val.bg = !val.bg;
						let all=this.list.every(data=>{
							return data.bg===true;
						})
						if(all){
							this.checkAll=true;
						}else{
							this.checkAll=false;
						}
						// console.log(all)
						return
					}
					
				}
				
			},
			allChecked(bg){
				for(let val of this.list){
					val.bg=!bg;
				}
				this.checkAll=!bg;
			},
			add(id){
				for(let val of this.list){
					if(val.id==id){
						if(val.num>=20){
							return
						}
						val.num=val.num+1;
					}
				}
			},
			sub(id){
				for(let val of this.list){
					if(val.id==id){
						if(val.num<=1){
							return
						}
						val.num=val.num-1;
					}
				}
			},
			del(id){
				for(let val of this.list){
					if(val.id==id){
						this.list.splice(this.list.indexOf(val),1);
						return
					}
				}
			}
		},
		computed: {
			allPrice() {
				let all = 0;
				for (let val of this.list) {
					if (val.bg) {
						all += val.num * val.price;
					}
				}
				return all;
			}
		}
	}
</script>

<style lang="less" scoped>
	.content {
			display: flex;
			flex-direction: column;
			align-items: center;
			padding: 0 20rpx;
			.shopchar {
				width: 100%;
			}
	
			.footall {
				position: fixed;
				bottom: 0;
				left: 0;
				background-color: #eee;
				width: 100%;
				height: 90rpx;
				display: flex;
				justify-content: flex-end;
				align-items: center;
	
				.close {
					background-color: #DD524D;
					color: #fff;
					height: 100%;
					width: 160rpx;
					display: flex;
					align-items: center;
					justify-content: center;
				}
	
				.footAll-price {
					margin-right: 20rpx;
	
					.all-price {
						color: #DD524D;
					}
				}
			}
	
			.table {
				width: 100%;
				display: flex;
				flex-direction: column;
				font-size: 30rpx;
				.tbody {
					.tr {
						display: flex;
						justify-content: space-between;
						align-items: center;
						margin: 10rpx 0;
	
						image {
							width: 160rpx;
							height: 140rpx;
						}
	
						.buttons {
							width: 80rpx;
							display: flex;
							flex-direction: column;
							align-items: center;
	
							/deep/uni-button[size=mini] {
								padding: 3rpx 20rpx;
	
								.sub {
									/deep/uni-button[size=mini] {
										padding: 3rpx 25rpx;
									}
								}
							}
	
							.good-price {
								text-align: center;
							}
	
							.btnbox {
								box-sizing: border-box;
								width: 60rpx;
								display: flex;
								justify-content: center;
							}
						}
	
						.delbox-out {
							display: flex;
							flex-direction: column;
							justify-content: center;
							align-items: center;
							width: 120rpx;
	
							.delbox {
								/deep/uni-button[size=mini] {
									padding: 10rpx 20rpx;
								}
							}
	
						}
	
						.goodsinof {
							flex: 1;
							padding-left: 10rpx;
							display: flex;
							flex-direction: column;
	
							.good-title {
								font-size: 30rpx;
								color: #333333;
							}
	
							.goods-price {
								font-size: 27rpx;
	
								.goods-price-in {
									font-size: 36rpx;
									color: #DD524D;
									font-weight: bold;
								}
							}
	
							.goods-old {
								font-size: 26rpx;
								color: #808080;
	
								.del-old {
									text-decoration: line-through;
								}
							}
						}
					}
				}
			}
	
			.shopchar-title {
				width: 100%;
				display: flex;
				justify-content: space-around;
	
				.allchecked {
					display: flex;
					justify-content: space-between;
	
					.allchecked-in {}
				}
	
			}
		}
	
</style>
