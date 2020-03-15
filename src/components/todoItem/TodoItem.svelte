<li class="todo-list-item">
  <div class="todo-item">
    <TodoIcon
      bind:done
      on:changeToDoing={ changeToDoing }
      on:changeToDone={ changeToDone }
    />
    <TodoTitle
      bind:title
      on:clickTodoItem={ clickTodoItem }
    />
  </div>
</li>

<script>
  import TodoIcon from './todoItemBody/TodoIcon.svelte'
  import TodoTitle from './todoItemBody/TodoTitle.svelte'
  import { createEventDispatcher } from 'svelte';

  export let id = ''
  export let title = ''
  export let done = false

  const dispatch = createEventDispatcher()

  function changeToDoing () {
    dispatch('changeToDoing', {id})
  }

  function changeToDone () {
    dispatch('changeToDone', {id}
    )
  }

  function clickTodoItem() {
    dispatch('showTodoDetails', {id})
  }
</script>

<style>
  .todo-list-item {
    padding: 0 3rem;
  }

  .todo-item {
    display: flex;
    height: 3rem;
    align-items: center;
    position: relative;
  }

  .todo-list-item + .todo-list-item {
    margin-top: 30px;
  }
</style>