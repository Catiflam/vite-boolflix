<script>
import { poster } from "./data/static";

export default {
	props: {
		cardInfo: Object,
	},
	computed: {
		hasFlag() {
			const allowedFlags = ["En", "it", "us"];
			return allowedFlags.includes(this.cardInfo.language);
		},

		flagSrc() {
			const flagUrl = new URL(`../../assets/img/${this.cardInfo.language}.png`, import.meta.url);
			return flagUrl.href;
		},

		posterSrc() {
			if (!this.cardInfo.posterPath) return "path to img default";
			return `${poster.baseUrl}${poster.size}${this.cardInfo.posterPath}`;
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
							{{ cardInfo.original_title }}
						</li>
						<li v-if="hasFlag">
							<img :src="flagSrc" :alt="cardInfo.language" />
						</li>
						<li>
							{{ cardInfo.vote }}
						</li>
						<li>
							<img :src="posterSrc" alt="" />
						</li>
					</ul>
				</h5>
			</div>
		</div>
	</div>
</template>

<style lang="scss" scoped></style>
