<template>
	<section>
		<div class="flex flex-col items-center justify-center p-8 ">
			<ImgLuckyWheel
				ref="wheel"
				class="w-96 h-96"
			/>
		</div>

	</section>
</template>

<script>
// import ImgLuckyWheel from "~/assets/icons/lucky_wheel.svg?inline";
import ImgLuckyWheel from "~/assets/icons/img_lucky_wheel.svg?inline";
export default {
	components: {
		ImgLuckyWheel,
	},

	data() {
		return {
			wheel: null,
			active: null,
			btnSpin: null,
			spinWheel: null,
			// tween: null,
			gifts: [
				{
					id: 1,
					amount: "jackpot",
					range: [0, 10],
				},
				{
					id: 2,
					amount: "1",
					range: [11, 54],
				},
				{
					id: 3,
					amount: "15",
					range: [55, 99],
				},
				{
					id: 4,
					amount: "5",
					range: [100, 144],
				},
				{
					id: 5,
					amount: "13",
					range: [145, 189],
				},
				{
					id: 6,
					amount: "7",
					range: [190, 234],
				},
				{
					id: 7,
					amount: "11",
					range: [235, 279],
				},
				,
				{
					id: 8,
					amount: "9",
					range: [280, 324],
				},
				,
				{
					id: 9,
					amount: "3",
					range: [325, 360],
				},
			],
		};
	},

	methods: {
		getRandomInt(min, max) {
			return Math.floor(Math.random() * (max - min + 1)) + min;
		},

		initWheel() {
			console.debug("initWheel");
			this.wheel = this.$refs.wheel.querySelector(".wheel");
			this.active = this.$refs.wheel.querySelector(".active");
			this.btnSpin = this.$refs.wheel.querySelector(".spin");
			this.spinWheel = this.$gsap.timeline();
		},

		initTween(rotation) {
			this.tween = null;
			this.tween = this.$gsap.core.Tween.to(this.wheel, 5, {
				rotation: rotation + "_cw",
				transformOrigin: "50% 50%",
				ease: "Power4.easeOut",
				repeatRefresh: true,
				paused: true,
			});
		},
	},

	mounted() {
		this.$nextTick(() => {
			this.initWheel();
			//
			var tween;
			var oldRotation = 0;
			var rotation = 0;

			console.debug("renew tween");

			this.btnSpin.addEventListener("click", () => {
				const giftIdx = Math.floor(Math.random() * 9);
				const gift = this.gifts[giftIdx];
				console.debug("gift", giftIdx, gift);
				const mediumRotation = (gift.range[0] + gift.range[1]) / 2;

				console.debug("mediumRotation", mediumRotation);
				console.debug("click to ", gift.amount);
				rotation = 4 * 360 + 360 - mediumRotation + 32;
				// var test = this.$gsap.core.Tween.to(this.wheel, 5, {
				// 	rotation: rotation + "_cw",
				// 	transformOrigin: "50% 50%",
				// 	ease: "Power4.easeOut",
				// 	onComplete: () => {
				// 		// test.set(this.wheel, {
				// 		// 	rotation: 122,
				// 		// });
				// 	},
				// });

				if (tween) {
					oldRotation = 360 - mediumRotation + 32;
					rotation = 360 - mediumRotation + 32 + (360 - oldRotation);
					console.debug("run vao day", rotation, tween);
					// tween.to(this.wheel, 5, {
					// 	rotation: rotation + "_cw",
					// 	transformOrigin: "50% 50%",
					// 	ease: "Power4.easeOut",
					// 	repeatRefresh: true,
					// });
					// tween.updateTo({
					// 	rotation: rotation,
					// });

					console.debug("tween", tween.vars);
					tween.set(this.wheel, { rotation });
					console.debug("tween", tween.vars);
					tween.restart();
				} else {
					rotation = 360 - mediumRotation + 32;
					console.debug("renew tween", rotation);
					tween = this.$gsap.core.Tween.to(this.wheel, 5, {
						rotation: rotation + "_cw",
						transformOrigin: "50% 50%",
						ease: "Power4.easeOut",
						repeatRefresh: true,
					});
				}
			});
		});
	},
};
</script>

<style scoped>
.luckywheel {
	margin: 40px auto;
	width: 50%;
	height: 50%;
}
</style>
