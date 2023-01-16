<template>
	<div>
		<p>{{ ActiveTodoItems.length }} items left</p>
		<ol v-if="showAll == true">
			<li v-for="(todoItem, index) in todoItems" :key="index">
				<span v-if="todoItem.completed == true">
					<input type="checkbox" @change="checkBoxClick(index)" checked />
					{{ todoItem }}
					<button @click="clearBtnClick(index)">clear</button>
				</span>
				<span v-else>
					<input type="checkbox" @change="checkBoxClick(index)" />
					{{ todoItem }}
					<button @click="clearBtnClick(index)">clear</button>
				</span>
			</li>
		</ol>
		<ol v-if="showActive == true">
			<li v-for="(ActivetodoItem, index) in ActiveTodoItems" :key="index">
				<span>
					<input type="checkbox" @change="checkBoxClick(index)" />
					{{ ActivetodoItem }}
					<button @click="clearBtnClick(index)">clear</button>
				</span>
			</li>
		</ol>
		<ol v-if="showCompleted == true">
			<li v-for="(CompletedTodoItem, index) in CompletedTodoItems" :key="index">
				<span>
					<input type="checkbox" @change="checkBoxClick(index)" checked />
					{{ CompletedTodoItem }}
					<button @click="clearBtnClick(index)">clear</button>
				</span>
			</li>
		</ol>
	</div>
</template>

<script>
export default {
	name: 'todolist',
	props: [
		'childValue',
		'childActiveValue',
		'childCompletedValue',
		'showAll',
		'showActive',
		'showCompleted',
	],
	data() {
		return {};
	},
	computed: {
		todoItems() {
			return this.childValue;
		},
		ActiveTodoItems() {
			return this.childActiveValue;
		},
		CompletedTodoItems() {
			return this.childCompletedValue;
		},
	},
	mounted() {},
	methods: {
		checkBoxClick(chxId) {
			this.$emit('checkBoxClick', chxId);
		},
		clearBtnClick(btnId) {
			console.log('clear');
			this.$emit('clearBtnClick', btnId);
		},
	},
};
</script>

<style></style>
