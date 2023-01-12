<template>
	<div>
		<ul>
			<li>{{ childValue.title }}</li>
			<!-- <li v-for="todoItem in todoItems" :key="todoItem.id">
				<input type="checkbox" :id="todoItem.id" />
				<label :for="todoItem.id"
					><p class="title">{{ todoItem.title }}</p></label
				>
			</li> -->
		</ul>
	</div>
</template>

<script>
export default {
	name: 'todolist',
	props: ['childValue'],
	data() {
		return {
			todoItems: [],
		};
	},
	created() {
		this.todoItems = JSON.parse(localStorage.getItem('todos-vuejs'));
		console.log('child', this.childValue);
		// 	console.log('list', this.todoItems.length);
		// if (localStorage.length > 0) {

		// for (var i = 0; i < this.todoItems.length; i++) {

		// }

		// for (var i = 0; i < localStorage.length; i++) {
		// 	if (localStorage.key(i) !== 'loglevel:webpack-dev-server') {
		// 		this.todoItems.push(localStorage.getItem(localStorage.key(i)));
		// 	}
		// }
		// }
	},
};
</script>

<style>
.todolist {
	font-size: 10px;
}
</style>
