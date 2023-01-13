<template>
	<div>
		<p v-for="(todoItem, index) in todoItems" :key="index">
			{{ todoItem.title }}
			<button v-on:click="deleteList(index)">delete</button>
		</p>
	</div>
</template>

<script>
export default {
	name: 'todolist',
	props: ['childValue'],
	data() {
		return {};
	},
	computed: {
		todoItems() {
			return this.childValue;
		},
	},
	mounted() {},
	methods: {
		deleteList(id) {
			this.$emit('change', id);
		},
	},
};
</script>

<style></style>
