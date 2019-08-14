<template>
	<view class="content">
		<div v-for="item in items">
			<p>{{item.x}}{{item.op1}}{{item.y}}{{item.op2}}{{item.z}}=<span v-if="item.seen"> {{item.res}}</span></p>
			<p><input type="text" v-model="item.doRes" /></p>
		</div>
		<button type="primary" @click="getTi(5)">craete</button>
		<button type="warn" @click="score">score</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				items: [],
				myScore: 0
			}
		},
		onLoad() {
			this.getTi(5);
		},
		methods: {
			test() {
				var arr = [2, 56, 34, 87];
				console.log(arr);
				var arr2 = this.mySort(arr);
				console.log(arr2);
			},
			getTi(num) {
				this.items = []; //清空
				var stop = false;
				var i = 0;
				while (!stop) {
					var ti = this.createTi();
					if (ti != null) {
						this.items.push(ti);
						i++;
					}
					if (i == num) {
						stop = true;
					}
				}
			},
			score() {

				var tis = this.items;
				for (var i = 0; i < tis.length; i++) {
					tis[i].seen = true;
					if (tis[i].res == tis[i].doRes) {
						this.myScore += 20;
					}
				}
				uni.showToast({
					title: '得分：' + this.myScore
				});
			},
			//创建题目
			createTi() {
				var x, y, z, op1, op2, res;
				var doRes = '';
				var arr = [];
				//初始化3个数
				for (var i = 0; i < 3; i++) {
					x = this.getRandomNum();
					y = this.getRandomNum();
					z = this.getRandomNum();
				}
				if (0 < (x + y + z) && (x + y + z) < 100) {
					op1 = "+";
					op2 = '+';
					res = x + y + z;
				} else if (0 < (x + y - z) && (x + y - z) < 100) {
					op1 = "+";
					op2 = '-';
					res = x + y - z;
				} else if (0 < (x - y + z) && (x - y + z) < 100) {
					op1 = "-";
					op2 = '+';
					res = x - y + z;

				} else if (0 < (x - y - z) && (x - y - z) < 100) {
					op1 = "-";
					op2 = '-';
					res = x - y - z;
				} else {
					return null;
				}

				return {
					x: x,
					y: y,
					z: z,
					op1: op1,
					op2: op2,
					res: res,
					doRes: doRes,
					seen: false
				}
			},
			//获取随机数
			getRandomNum() {
				return Math.ceil(Math.random() * 100);
			}
		}
	}
</script>

<style>
</style>
