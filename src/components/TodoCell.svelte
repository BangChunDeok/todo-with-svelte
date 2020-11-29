<script>
  import { createEventDispatcher } from 'svelte'
  import DeleteIcon from '@/Icons/delete.svelte'

  export let todo = { text: '', unique: '' }
  const dispatch = createEventDispatcher()

  function onClickDelete() {
    dispatch('delete', todo)
  }
</script>

<div class="todo-cell">
  <span>{ todo.text }</span>
  <button on:click={onClickDelete}>
    <DeleteIcon />
  </button>
</div>

<style>
.todo-cell {
  display: flex;
  align-items: center;
  justify-content: center;

  width: 100%;
  padding: 16px;
  margin-top: 16px;
  border: 1px solid #dee2e6;
  border-radius: 3rem;

	font-size: 1.5em;
	line-height: 1.5em;
  text-align: center;
  background-color: white;
}

span {
  width: 100%;
  height: 100%;
  margin-left: auto;
  overflow: hidden;
  text-overflow:ellipsis;
  white-space:nowrap;
}

button {
  display: flex;
  justify-content: center;
  align-items: center;

  width: 2.5rem;
  height: 2.5rem;
  padding: 8px;
  margin-left: auto;
  margin-right: 8px;
  border: 1px solid #dee2e6;
  border-radius: 50%;
}
</style>