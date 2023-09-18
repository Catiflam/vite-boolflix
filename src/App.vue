<script>
import axios from "axios";
import { store } from "./components/data/store";

import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";

const api_key = "20b4b109d496b6449e7be57748b5e994";
export default {
	data() {
		return {
			store,
		};
	},

	components: { AppHeader, AppMain },

	methods: {
		fetchMovies(term) {
			axios
				.get("https://api.themoviedb.org/3/search/movie?", {
					params: {
						query: term,
						api_key,
					},
				})
				.then((response) => {
					console.log(response);
					store.movies = response.data.results.map((movie) => {
						const { id, title, original_title, original_language, vote_average } = movie;
						return { id, name: title, title: original_title, language: original_language, vote: Math.ceil(vote_average / 2) };
					});
				});
		},

		fetchSeries(term) {
			axios
				.get("https://api.themoviedb.org/3/search/tv?", {
					params: {
						query: term,
						api_key,
					},
				})
				.then((response) => {
					console.log(response);
					store.series = response.data.results.map((serie) => {
						const { id, title, original_title, original_language, vote_average } = serie;
						return { id, name: title, title: original_title, language: original_language, vote: Math.ceil(vote_average / 2) };
					});
				});
		},

		handleSearc(term) {
			if (!term) return;
			this.fetchMovies(term);
			this.fetchSeries(term);
		},
	},
};
</script>

<template>
	<AppHeader @start-search="handleSearc" />

	<AppMain />
</template>

<style lang="scss">
@use "./assets/attribute/style.scss" as *;
</style>
