<div on:click={ clickTodoItem } class="todo-title-area">
  <label class="todo-title">{ title }</label>
</div>

<script>
  import { createEventDispatcher } from 'svelte'

  export let title = false
  const dispatch = createEventDispatcher()

  function clickTodoItem() {
    dispatch('clickTodoItem')
  }
</script>

<style>
  .todo-title-area {
    width: 100%;
    height: 100%;
    border: 5px solid #BDBDBD;
    border-radius: 5px;
  }

  .todo-title {
    font-size: 2rem;
    color: #616161;
    user-select: none;
  }
</style>