<template>
	<div id="app">
		<h1>Todo App</h1>
		<AddTodo :addTodo="addTodo" :clearTodos="clearTodos" />
		<div class="todos">
			<TodoItem
				v-for="todo in todos"
				:key="todo.id"
				:todo="todo"
				:removeTodo="removeTodo"
				:changeTodo="changeTodo"
			/>
		</div>
	</div>
</template>

<script>
import TodoItem from "./components/TodoItem";
import AddTodo from "./components/AddTodo";

export default {
	name: "App",
	components: {
		TodoItem,
		AddTodo,
	},
	data() {
		return {
			todos: [],
		};
	},
	methods: {
		removeTodo(id) {
			this.todos = this.todos.filter((todo) => todo.id != id);
			window.localStorage.setItem("todos", JSON.stringify(this.todos));
		},
		changeTodo(id, checked) {
			this.todos.forEach((todo) => {
				if (todo.id == id) {
					todo.finished = checked;
				}
			});
			window.localStorage.setItem("todos", JSON.stringify(this.todos));
		},
		addTodo(name) {
			if (name) {
				const todosLength = this.todos.length;
				const currentId =
					todosLength > 0 ? this.todos[todosLength - 1].id + 1 : 0;
				this.todos.push({ id: currentId, name: name, finished: false });
				window.localStorage.setItem(
					"todos",
					JSON.stringify(this.todos)
				);
			}
		},
		clearTodos() {
			this.todos = [];
			window.localStorage.clear();
		},
	},
	created() {
		this.todos = JSON.parse(window.localStorage.getItem("todos"));
		if (!this.todos) {
			this.todos = [];
		}
	},
};
</script>

<style>
body {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #f3f9ff;
	background-color: #141618;
	margin: 0px;
	margin-top: 60px;
}

h1 {
	font-size: 45px;
}

.todos {
	display: flex;
	align-items: center;
	justify-content: center;
	flex-direction: column;
	margin-top: 50px;
}

@media only screen and (max-width: 600px) {
	body {
		margin-top: 10px;
	}
}
</style>
