<template>
	<div class="todo">
		<input type="text" v-model="newTodoItem" @keyup.enter="addTodo" />
		<TodoList
			:childValue="Basket"
			:childActiveValue="activeBasket"
			:childCompletedValue="completedBasket"
			:showAll="showAll"
			:showActive="showActive"
			:showCompleted="showCompleted"
			@clearBtnClick="clearBtnClick"
			@checkBoxClick="checkBoxClick"
		></TodoList>
		<div>
			<button class="showAll" @click="showAllTodo">All</button>
			<button class="showActive" @click="showActiveTodo">Active</button>
			<button class="showCompleted" @click="showCompletedTodo">
				Completed
			</button>
		</div>
		<button class="clear" @click="clearTodo">Clear All</button>
		<button class="clearTrue" @click="clearTrueTodo">Clear completed</button>
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
			activeBasket: [],
			completedBasket: [],
			TodoBasket: JSON.parse(localStorage.getItem('todos-vuejs')) || [],
			showAll: true,
			showActive: false,
			showCompleted: false,
		};
	},
	components: {
		TodoList,
	},
	created() {
		this.Basket = this.TodoBasket;
	},
	mounted() {},
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
		checkBoxClick(chxId) {
			this.Basket[chxId].completed = !this.Basket[chxId].completed;
			localStorage.setItem(this.keyName, JSON.stringify(this.Basket));
		},
		clearBtnClick(btnId) {
			this.Basket.splice(btnId, 1);
			localStorage.setItem(this.keyName, JSON.stringify(this.Basket));
		},
		clearTodo() {
			this.Basket.splice(0);
			localStorage.clear();
		},
		clearTrueTodo() {
			for (let i = 0; i < this.Basket.length; i++) {
				if (this.Basket[i].completed == true) {
					this.Basket.splice(i, 1);
					i--;
				}
			}
			localStorage.setItem(this.keyName, JSON.stringify(this.Basket));
		},
		showAllTodo() {
			this.showAll = true;
			this.showActive = false;
			this.showCompleted = false;
			this.Basket = JSON.parse(localStorage.getItem('todos-vuejs')) || [];
		},
		showActiveTodo() {
			this.showAll = false;
			this.showActive = true;
			this.showCompleted = false;
			this.Basket = JSON.parse(localStorage.getItem('todos-vuejs')) || [];
			for (let i = 0; i < this.Basket.length; i++) {
				if (this.Basket[i].completed == true) {
					this.Basket.splice(i, 1);
					i--;
				}
			}
			this.activeBasket = this.Basket;
		},
		showCompletedTodo() {
			this.showAll = false;
			this.showActive = false;
			this.showCompleted = true;
			this.Basket = JSON.parse(localStorage.getItem('todos-vuejs')) || [];
			for (let i = 0; i < this.Basket.length; i++) {
				if (this.Basket[i].completed != true) {
					this.Basket.splice(i, 1);
					i--;
				}
			}
			this.completedBasket = this.Basket;
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
