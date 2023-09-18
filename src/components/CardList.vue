<script>
import { store } from "./data/store";
import CardDetail from "./CardDetail.vue";
export default {
	data() {
		return {
			store,
		};
	},
	components: { CardDetail },
};
</script>

<template>
	<section>
		<h2>Movies</h2>
		<CardDetail v-for="movie in store.movies" :key="movie.id" :cardInfo="movie" />
	</section>

	<section>
		<h2>Tv Series</h2>
		<CardDetail v-for="serie in store.series" :key="serie.id" :cardInfo="serie" />
	</section>
</template>

<style lang="scss" scoped></style>
