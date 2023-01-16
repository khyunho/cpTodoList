<template>
	<div class="todo">
		<input type="text" v-model="newTodoItem" @keyup.enter="addTodo" />
		<TodoList
			:childValue="Basket"
			:countCompleted="count"
			@deleteBtnClick="deleteBtnClick"
			@checkBoxClick="checkBoxClick"
		></TodoList>
		<button class="clear" @click="clearTodo">Clear All</button>
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
			Basket: [],
			TodoBasket: JSON.parse(localStorage.getItem('todos-vuejs')) || [],
			count: 0,
		};
	},
	components: {
		TodoList,
	},
	created() {
		this.Basket = this.TodoBasket;
	},
	methods: {
		addTodo() {
			var idNum = this.Basket.length;
			const value = {
				id: idNum,
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
		},
		clearInput() {
			this.newTodoItem = '';
		},
		clearTodo() {
			this.Basket.splice(0);
			localStorage.clear();
		},
		checkBoxClick(chxId) {
			this.Basket[chxId].completed = !this.Basket[chxId].completed;
			localStorage.setItem(this.keyName, JSON.stringify(this.Basket));
			if (this.Basket[chxId].completed == true) {
				this.count += 1;
			} else {
				this.count -= 1;
			}
		},
		deleteBtnClick(btnId) {
			this.Basket.splice(btnId, 1);
			localStorage.setItem(this.keyName, JSON.stringify(this.Basket));
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
