<script>
export default {
	props: {
		cardInfo: Object,
	},
	computed: {
		hasFlag() {
			const allowedFlags = ["en", "it"];
			return allowedFlags.includes(this.cardInfo.language);
		},

		flagSrc() {
			const flagUrl = new URL(`./../assets/img/${this.cardInfo.language}.png`, import.meta.url);
			return flagUrl.href;
		},
	},
};
</script>

<template>
	<div class="container mt-5">
		<div class="card" style="width: 18rem">
			<div class="card-body">
				<h5 class="card-title">
					<ul>
						<li>
							{{ cardInfo.name }}
						</li>
						<li>
							{{ cardInfo.title }}
						</li>
						<li v-if="hasFlag">
							<img :src="flagSrc" :alt="cardInfo.language" />
						</li>
						<li>
							{{ cardInfo.vote }}
						</li>
						<li></li>
					</ul>
				</h5>
			</div>
		</div>
	</div>
</template>

<style lang="scss" scoped></style>
