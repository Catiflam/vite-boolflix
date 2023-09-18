<script>
import CardList from "./CardList.vue";
export default {
	data() {
		return {
			title: "appmain",
		};
	},
	components: { CardList },
};
</script>

<template>
	<div class="container mt-5">
		<h2>{{ title }}</h2>
		<CardList />
	</div>
</template>

<style lang="scss" scoped></style>
