<template>
	<button :class="mode">
		<slot></slot>
	</button>
</template>

<script>
	export default {
		props: ["mode"],
	};
</script>

<style scoped>
	button {
		padding: 0.6rem 1.25rem;
		font-family: inherit;
		background-color: #ff006a;
		border: 1px solid #ff006a;
		color: white;
		cursor: pointer;
		border-radius: 4px;
		transition: 0.3s;
	}

	button:hover,
	button:active {
		filter: brightness(0.85);
	}

	button.flat {
		background-color: transparent;
		color: #ff006a;
		border: none;
	}

	button.flat:hover,
	button.flat:active {
		background-color: #ff006a1e;
	}
</style>
