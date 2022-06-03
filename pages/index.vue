<template>
	<section>
		<!-- <LuckyWheel
			ref="myLucky"
			width="300px"
			height="300px"
			:prizes="prizes"
			:blocks="blocks"
			:buttons="buttons"
			@start="startCallback"
			@end="endCallback"
		/> -->
	</section>
</template>

<script>
import { LuckyWheel } from "lucky-canvas";
export default {
	name: "IndexPage",
	components: {
		LuckyWheel,
	},
	data() {
		return {
			blocks: [{ padding: "10px", background: "#869cfa" }],
			prizes: [
				{ background: "#e9e8fe", fonts: [{ text: "0" }] },
				{ background: "#b8c5f2", fonts: [{ text: "1" }] },
				{ background: "#e9e8fe", fonts: [{ text: "2" }] },
				{ background: "#b8c5f2", fonts: [{ text: "3" }] },
				{ background: "#e9e8fe", fonts: [{ text: "4" }] },
				{ background: "#b8c5f2", fonts: [{ text: "5" }] },
			],
			buttons: [
				{ radius: "40%", background: "#617df2" },
				{ radius: "35%", background: "#afc8ff" },
				{
					radius: "30%",
					background: "#869cfa",
					pointer: true,
					fonts: [{ text: "开始", top: "-10px" }],
				},
			],
		};
	},

	methods: {
		// 点击抽奖按钮会触发star回调
		startCallback() {
			// 调用抽奖组件的play方法开始游戏
			this.$refs.myLucky.play();
			// 模拟调用接口异步抽奖
			setTimeout(() => {
				// 假设后端返回的中奖索引是0
				const index = 0;
				// 调用stop停止旋转并传递中奖索引
				this.$refs.myLucky.stop(index);
			}, 3000);
		},
		// 抽奖结束会触发end回调
		endCallback(prize) {
			console.log(prize);
		},
	},
};
</script>
