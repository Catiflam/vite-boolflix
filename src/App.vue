<script>
import axios from "axios";

import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";

const api_key = "20b4b109d496b6449e7be57748b5e994";
export default {
	data() {
		return {
			movies: [],
		};
	},

	components: { AppHeader, AppMain },

	methods: {
		fetchMovies(term) {
			axios
				.get("https://api.themoviedb.org/3/search/movie", {
					params: {
						querry: term,
						api_key,
					},
				})
				.then((response) => {
					this.movies = response.data.results;
				});
		},
	},

	created() {
		this.fetchMovies();
	},
};
</script>

<template>
	<AppHeader @start-search="fetchMovies" />
	<ul>
		<li v-for="movie in movies">
			{{ movie }}
		</li>
	</ul>
	<AppMain />
</template>

<style lang="scss">
@use "./assets/attribute/style.scss" as *;
</style>
