<template>
	<the-header :title="'Learning Resources App'"></the-header>
	<the-resources></the-resources>
</template>

<script>
	import TheHeader from "./layouts/TheHeader";
	import TheResources from "./components/learning-resources/TheResources.vue";

	export default {
		components: {
			TheHeader,
			TheResources,
		},
	};
</script>

<style>
	@import url("https://fonts.googleapis.com/css2?family=Josefin+Sans&display=swap");

	* {
		box-sizing: border-box;
		font-family: "Josefin Sans", sans-serif;
	}

	body {
		margin: 0;
	}
</style>
