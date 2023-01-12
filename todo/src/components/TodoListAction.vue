<template>
	<div class="todo">
		<input type="text" v-model="newTodoItem" @keyup.enter="addTodo" />
		<TodoList :childValue="Basket"></TodoList>
	</div>
</template>

<script>
import TodoList from './TodoList.vue';
export default {
	name: 'todo',
	data() {
		return {
			keyName: 'todos-vuejs',
			newTodoItem: '',
			idNum: 0,
			Basket: [],
			TodoBasket: JSON.parse(localStorage.getItem('todos-vuejs')) || [],
		};
	},
	components: {
		TodoList,
	},
	mounted() {
		this.Basket = this.TodoBasket;
	},
	methods: {
		addTodo() {
			if (JSON.parse(localStorage.getItem('todos-vuejs')) == null) {
				this.idNum = 0;
			}
			// console.log('id', this.idNum);
			// console.log('title', this.newTodoItem);
			const value = {
				id: this.idNum,
				title: this.newTodoItem,
				completed: false,
			};
			if (this.newTodoItem == '') {
				this.clearInput();
			} else {
				this.idNum += 1;
				this.TodoBasket.push(value);
				localStorage.setItem(this.keyName, JSON.stringify(this.TodoBasket));
				this.clearInput();
				this.Basket = this.TodoBasket;
			}
			// console.log(JSON.parse(localStorage.getItem('todos-vuejs')));
		},
		clearInput() {
			this.newTodoItem = '';
		},
	},
};
</script>

<style>
.todo {
	font-size: 15px;
	text-align: center;
}
</style>
