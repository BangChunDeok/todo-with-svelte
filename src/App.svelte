<script>
	import { todos } from '@/store/todo.js'
	import TodoCell from './components/TodoCell.svelte'

	function onSubmitTodo() {
		$todos = [...$todos, {
			text: todo,
			unique: Date.now()
		}]
		todo = ''
	}

	function onDeleteTodo({ detail }) {
		$todos = $todos.filter((todo) => todo.unique !== detail.unique)
	}

	$: {
		localStorage.setItem('todos', JSON.stringify($todos))
	}

	const loadedData = JSON.parse(localStorage.getItem('todos'))
	if (loadedData) {
		$todos = loadedData
	}

	let todo = ''
</script>

<main id="app">
	<h1>
		Simple Svelte<br>
		Todo list
	</h1>
	<form on:submit|preventDefault={onSubmitTodo}>
		<input class="todo-input" bind:value={todo} placeholder="할 일을 입력해주세요!" />
	</form>
	{#each $todos as todo (todo.unique) }
		<TodoCell todo={todo} on:delete={onDeleteTodo} />
	{/each}
</main>

<style>
#app {
	display: flex;
	flex-direction: column;
	justify-content: center;
	max-width: 50rem;
	padding: 16px;
	margin: 0 auto;
}

h1 {
	text-align: center;
}

.todo-input {
	width: 100%;
	padding: 16px;
  border: 1px solid #dee2e6;
  border-radius: 3rem;
	font-size: 1.5em;
	text-align: center;
	background-color: white;
	margin-top: 16px;
}
</style>