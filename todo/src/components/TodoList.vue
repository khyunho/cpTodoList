<template>
	<div>
		<p>{{ todoItems.length }} items left</p>
		<ol>
			<li v-for="(todoItem, index) in todoItems" :key="index">
				<span v-if="todoItem.completed == true">
					<input type="checkbox" @change="checkBoxClick(index)" checked />
					{{ todoItem }}
					<button @click="deleteBtnClick(index)">delete</button>
				</span>
				<span v-else>
					<input type="checkbox" @change="checkBoxClick(index)" />
					{{ todoItem }}
					<button @click="deleteBtnClick(index)">delete</button>
				</span>
			</li>
		</ol>
		<!-- <p>{{ todoItems.length }} items left</p>
		<p v-for="(todoItem, index) in todoItems" :key="index">
			<input type="checkbox" v-model="completed" />
			{{ todoItem.title }}
			<button @click="deleteList(index)">delete</button>
		</p> -->
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
		checkBoxClick(chxId) {
			// console.log('check');
			this.$emit('checkBoxClick', chxId);
		},
		deleteBtnClick(btnId) {
			console.log('delete');
			this.$emit('deleteBtnClick', btnId);
		},
	},
};
</script>

<style></style>
