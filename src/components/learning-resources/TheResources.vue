<template>
	<base-card>
		<div class="nav-container">
			<base-button
				@click="setSelectedTab('stored-resources')"
				:mode="setResButtonMode"
			>
				Stored Resources
			</base-button>
			<base-button @click="setSelectedTab('add-resource')" :mode="setAddButtonMode">
				Add Resources
			</base-button>
		</div>
	</base-card>
	<component :is="selectedTab"></component>
</template>

<script>
	import StoredResources from "./StoredResources";
	import AddResource from "./AddResource";

	export default {
		components: {
			StoredResources,
			AddResource,
		},

		provide() {
			return {
				resources: this.storedResources,
				addResource: this.addResource,
				removeResource: this.removeResource,
			};
		},

		data() {
			return {
				selectedTab: "stored-resources",
				storedResources: [],
			};
		},

		computed: {
			setResButtonMode() {
				return this.selectedTab === "stored-resources" ? null : "flat";
			},

			setAddButtonMode() {
				return this.selectedTab === "add-resource" ? null : "flat";
			},
		},

		methods: {
			setSelectedTab(tab) {
				this.selectedTab = tab;
			},

			addResource(title, description, link) {
				let tempData = title.toLowerCase();
				tempData = tempData.replace(" ", "-");

				const newResource = {
					id: tempData,
					title: title,
					description: description,
					resourceUrl: link,
				};

				this.storedResources.unshift(newResource);
				this.updateLocalStorage();
				this.selectedTab = "stored-resources";
			},

			removeResource(id) {
				const resourceIndex = this.storedResources.findIndex(
					(resource) => resource.id === id
				);

				this.storedResources.splice(resourceIndex, 1);
				this.updateLocalStorage();
			},

			updateLocalStorage() {
				let tempData = JSON.stringify(this.storedResources);
				localStorage.setItem("storedResources", tempData);
			},
		},

		beforeMount() {
			let tempData;
			if (!localStorage.getItem("storedResources")) {
				tempData = [
					{
						id: "official-guide",
						title: "Official Guide",
						description: "The official Vue JS 3x documentation.",
						resourceUrl: "https://v3.vuejs.org/guide/introduction.html",
					},
					{
						id: "google",
						title: "Google",
						description: "Learn by searching on Google.",
						resourceUrl: "https://www.google.com/",
					},
				];
				tempData.forEach((item) => {
					this.storedResources.push(item);
				});
				tempData = JSON.stringify(tempData);
				localStorage.setItem("storedResources", tempData);
			} else {
				tempData = localStorage.getItem("storedResources");
				tempData = JSON.parse(tempData);

				tempData.forEach((item) => {
					this.storedResources.push(item);
				});
			}
		},
	};
</script>

<style>
	.nav-container {
		display: flex;
		justify-content: center;
		gap: 10px;
	}
</style>
