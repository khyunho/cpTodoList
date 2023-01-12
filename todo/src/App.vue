<template>
	<div>
		<Header></Header>
		<Todo></Todo>
		<Footer></Footer>
	</div>
</template>

<script>
import Header from './components/Header.vue';
import Todo from './components/TodoListAction.vue';
import Footer from './components/Footer.vue';
export default {
	name: 'App',
	components: {
		Header,
		Todo,
		Footer,
	},
};
</script>

<style></style>
