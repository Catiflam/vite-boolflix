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
					// console.log(response);
					store.movies = response.data.results.map((movie) => {
						const id = movie.id;
						const name = movie.title;
						const original_title = movie.original_title;
						const language = movie.original_language;
						const vote = Math.ceil(movie.vote_average / 2);
						const posterPath = movie.poster_path;

						return {
							id,
							name,
							original_title,
							language,
							vote,
							posterPath,
						};
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
						const id = serie.id;
						const name = serie.title;
						const original_title = serie.original_title;
						const language = serie.original_language;
						const vote = Math.ceil(serie.vote_average / 2);
						const posterPath = serie.poster_path;

						return {
							id,
							name,
							original_title,
							language,
							vote,
							posterPath,
						};
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
