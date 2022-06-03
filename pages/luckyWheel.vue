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

		controlWheel(rotation) {
			var currentRotation,
				lastRotation = 0,
				tolerance;
			console.debug("controlWheel", this.spinWheel);
			this.spinWheel.to(this.wheel, 2, {
				rotation: rotation,
				transformOrigin: "50% 50%",
				ease: "Power4.easeOut",
				onUpdate: () => {
					console.debug("data", this);
					tolerance = currentRotation - lastRotation;
					if (Math.round(currentRotation) % (360 / 12) <= tolerance) {
						if (indicator.progress() > 0.2 || indicator.progress() === 0) {
							indicator.play(0);
						}
					}
					lastRotation = currentRotation;
				},
			});
			this.spinWheel.add("end");
		},
	},

	mounted() {
		this.$nextTick(() => {
			this.initWheel();
			//
			this.btnSpin.addEventListener("click", () => {
				const giftIdx = Math.floor(Math.random() * 9);
				const gift = this.gifts[giftIdx];
				console.debug("gift", giftIdx, gift);
				const mediumRotation = (gift.range[0] + gift.range[1]) / 2;
				console.debug("mediumRotation", mediumRotation);
				console.debug("click to ", gift.amount);
				var rotation = 4 * 360 + (360 - mediumRotation + 32);
				this.$gsap.core.Tween.to(this.wheel, 5, {
					rotation: rotation + "_cw",
					transformOrigin: "50% 50%",
					ease: "Power4.easeOut",
					repeatRefresh: true,
					onComplete: () => {
						console.debug("completed", rotation);
						rotation = 0;
					},
				});
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
