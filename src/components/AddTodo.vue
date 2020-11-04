<template>
	<div class="addtodo">
		<input
			type="text"
			placeholder="Name"
			v-model="name"
			v-on:keydown.enter="handleAdd(name)"
		/>
		<div>
			<button v-on:click="handleAdd(name)">Add</button>
			<button v-on:click="clearTodos()">Clear</button>
		</div>
	</div>
</template>

<script>
export default {
	name: "AddTodo",
	props: {
		addTodo: Function,
		clearTodos: Function,
	},
	data() {
		return {
			name: "",
		};
	},
	methods: {
		handleAdd(name) {
			this.addTodo(name);
			this.name = "";
		},
	},
};
</script>

<style scoped>
.addtodo {
	display: flex;
	align-items: center;
	justify-content: center;
	flex-direction: column;
}

input {
	outline: none;
	background-color: #141618;
	color: #e8effb;
	padding: 10px;
	border: 2px solid #5c6370;
	font-size: 20px;
	transition: 0.5s;
}
input:focus {
	transition: 0.5s;
	border-color: #a1aec5;
}

button {
	border: 2px solid #5c6370;
	background-color: #1e2124;
	color: #e8effb;
	padding: 10px;
	margin: 10px;
	outline: none;
	cursor: pointer;
	font-size: 19px;
	transition: 0.2s;
}
button:hover {
	transition: 0.2s;
	border-color: #818c9e;
}
button:active {
	transition: 0.2s;
	border-color: #4e545f;
}
</style>