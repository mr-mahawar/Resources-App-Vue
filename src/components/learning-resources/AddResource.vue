<template>
	<base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="closeDialog">
		<template #default>
			<p>One of the Inputs value is Invalid!</p>
			<p>Please make sure to enter appropriate value in the fields.</p>
		</template>
		<template #actions>
			<base-button @click="closeDialog">Okay</base-button>
		</template>
	</base-dialog>
	<base-card>
		<form @submit.prevent="submitForm">
			<div class="form-element">
				<label for="title">Title</label>
				<input
					type="text"
					id="title"
					name="title"
					placeholder="Resource Title"
					ref="titleInput"
					autocomplete="off"
				/>
			</div>
			<div class="form-element">
				<label for="description">Description</label>
				<textarea
					row="3"
					id="description"
					name="description"
					placeholder="Short Description"
					ref="descriptionInput"
					autocomplete="off"
				/>
			</div>
			<div class="form-element">
				<label for="link">Link</label>
				<input
					type="url"
					id="link"
					name="link"
					placeholder="Link to Resource"
					ref="linkInput"
					autocomplete="off"
				/>
			</div>
			<div class="form-button">
				<base-button>Add Resource</base-button>
			</div>
		</form>
	</base-card>
</template>

<script>
	export default {
		inject: ["addResource"],

		data() {
			return {
				inputIsInvalid: false,
			};
		},

		methods: {
			submitForm() {
				const enteredTitle = this.$refs.titleInput.value;
				const enteredDescription = this.$refs.descriptionInput.value;
				const enteredLink = this.$refs.linkInput.value;

				if (
					enteredTitle.trim() === "" ||
					enteredDescription.trim() === "" ||
					enteredTitle.trim() === ""
				) {
					this.inputIsInvalid = true;
					return;
				}

				this.addResource(enteredTitle, enteredDescription, enteredLink);
			},

			closeDialog() {
				this.inputIsInvalid = false;
			},
		},
	};
</script>

<style scoped>
	label {
		font-weight: bold;
		font-size: 1.1rem;
		display: block;
		margin-bottom: 0.5rem;
	}

	input,
	textarea {
		display: block;
		width: 100%;
		font: inherit;
		padding: 0.25rem;
		border: 1px solid #ccc;
		border-radius: 4px;
		resize: none;
		transition: 0.3s;
	}

	input::placeholder,
	textarea::placeholder {
		font-size: 0.8rem;
		transition: 0.3s;
	}

	input:focus,
	textarea:focus {
		outline: none;
		border-color: #510061;
		background-color: #f7ebff;
	}

	input:focus::placeholder,
	textarea:focus::placeholder {
		font-size: 0.6rem;
	}

	.form-element {
		margin: 1rem 0;
	}

	.form-button {
		display: flex;
		justify-content: center;
	}
</style>
