<div 
  class={ "todo-check-icon " + (done ? "done-icon-background" : "doing-icon-background") }
  on:click={ changeDone }
>
  <Icon { icon } />
</div>

<script>
  import Icon from 'fa-svelte'
  import { faCheck } from '@fortawesome/free-solid-svg-icons/faCheck'
  import { createEventDispatcher } from 'svelte';

  export let done = false
  const icon = faCheck
  const dispatch = createEventDispatcher()

  function changeDone () {
    if (done) {
      dispatch('changeToDoing')
    } else {
      dispatch('changeToDone')
    }
  }
</script>

<style>
  .todo-check-icon {
    color: #fff;
    font-size: 3rem;
    padding: .5rem;
    width: 3rem;
    height: 3rem;
    border-radius: 3rem;
    position: absolute;
    left: -1rem;
    cursor: pointer;
    transition: background .5s;
  }

  .done-icon-background {
    background: #4EC34A;
  }

  .doing-icon-background {
    background: #BDBDBD;
  }
</style>