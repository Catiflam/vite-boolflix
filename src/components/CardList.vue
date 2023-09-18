<script>
import CardDetail from "./CardDetail.vue";
export default {
	data() {
		return {
			title: "cardlist",
		};
	},
	components: { CardDetail },
};
</script>

<template>
	<h3>{{ title }}</h3>
	<CardDetail v-for="i in 5" />
</template>

<style lang="scss" scoped></style>
