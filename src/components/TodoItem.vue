<template>
	<div class="todoitem">
		<h2 :class="checkStyle" v-on:click="handleClick">
			{{ todo.name }}
		</h2>
		<button class="remove" v-on:click="removeTodo(todo.id)">x</button>
	</div>
</template>

<script>
export default {
	name: "TodoItem",
	props: {
		todo: Object,
		removeTodo: Function,
		changeTodo: Function,
	},
	data() {
		return {
			checked: false,
			checkStyle: "",
		};
	},
	methods: {
		handleClick() {
			this.checked = !this.checked;
			this.checkStyle = this.checked ? "crossed" : "";
			this.changeTodo(this.todo.id, this.checked);
		},
	},
	created() {
		this.checked = this.todo.finished;
		this.checkStyle = this.checked ? "crossed" : "";
	},
};
</script>

<style scoped>
input[type="checkbox"] {
	margin-right: 10px;
	margin-left: 20px;
}

h2 {
	margin-left: 10px;
	font-weight: 300;
	font-size: 24px;
	cursor: pointer;
}

.crossed {
	text-decoration: line-through;
}

.remove {
	outline: none;
	font-size: 20px;
	border: none;
	border-radius: 50%;
	background-color: #da4f4f;
	color: #fffefe;
	padding: 5px 12px;
	text-align: center;
	margin-right: 10px;
	cursor: pointer;
}

.todoitem {
	background-color: #20262c;
	border-bottom: 2px solid #535860;
	width: 100%;
	display: flex;
	align-items: center;
	justify-content: space-between;
}

@media only screen and (max-width: 600px) {
	h2 {
		font-size: 20px;
	}
	.remove {
		font-size: 18px;
	}
}
</style>
