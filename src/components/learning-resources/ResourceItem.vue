<template>
	<li>
		<base-card>
			<div class="header">
				<h2>{{ item.title }}</h2>
				<base-button mode="flat" @click="removeResource(item.id)">
					Delete
				</base-button>
			</div>
			<div class="description">{{ item.description }}</div>
			<div class="resource-url">
				<a href="item.resourceUrl" target="_blank" title="item.title">
					Go to Resource
				</a>
			</div>
		</base-card>
	</li>
</template>

<script>
	export default {
		props: ["item"],

		inject: ["removeResource"],
	};
</script>

<style scoped>
	li {
		margin: auto;
		max-width: 40rem;
	}

	.header {
		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	.header h2 {
		font-size: 1.3rem;
		margin: 0.75rem 0;
	}

	.decription {
		margin: 0.5rem 0;
	}

	.resource-url {
		margin-top: 10px;
	}

	.resource-url a {
		text-decoration: none;
		color: #ff006a;
		transition: 0.3s;
	}

	.resource-url a:hover,
	.resource-url a:active {
		filter: brightness(0.8);
	}
</style>
