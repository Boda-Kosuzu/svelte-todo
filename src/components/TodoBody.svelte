<main>
  <div class="todo-body">
    <div class="todo-items-body">
      <ul class="todo-items-list">
        {#each todoList as item}
          <TodoItem
            { ...item }
            on:changeToDoing={ changeToDoing }
            on:changeToDone={ changeToDone }
            on:showTodoDetails={ showTodoDetails }
          />
        {/each}
      </ul>
    </div>
    <div class="todo-button-area">
      <button
        class="add-button"
        on:click={ showRegisterModal }
      >
        登録
      </button>
    </div>
  </div>
  {#if displayRegisterDialog}
    <RegisterModal
       on:closeModal={ closeRegisterModal }
       on:register={ registerNewItem }
    />
  {/if}

  {#if displayUpdateDialog}
    <UpdateModal
       on:closeModal={ closeUpdateModal }
       on:update={ updateItem }
       bind:todoItemDetails
    />
  {/if}
</main>

<script>
  import TodoItem from './todoItem/TodoItem.svelte'
  import RegisterModal from './todoModal/RegisterModal.svelte';
  import UpdateModal from './todoModal/UpdateModal.svelte';

  let displayRegisterDialog = false
  let displayUpdateDialog = false
  let todoItemDetails = {}

  let todoList = [
    {
      id: Math.random().toString(32).substring(2),
      title: 'Todo',
      done: false,
      description: 'これはテスト用のコンテンツです。'
    }
  ]

  function changeToDoing (event) {
    const targetIndex = todoList.findIndex(item => {
      return item.id === event.detail.id
    })
    
    const target = {
      ...todoList[targetIndex],
      done: false
    }

    todoList[targetIndex] = target
  }

  function changeToDone (event) {
    const targetIndex = todoList.findIndex(item => {
      return item.id === event.detail.id
    })

    const target = {
      ...todoList[targetIndex],
      done: true
    }

    todoList[targetIndex] = target
  }

  function registerNewItem(event) {
    const item = {
      ...event.detail,
      id: Math.random().toString(32).substring(2),
      done: false
    }

    todoList = [...todoList, item]

    closeRegisterModal()
  }

  function showRegisterModal() {
    displayRegisterDialog = true
  }

  function closeRegisterModal() {
    displayRegisterDialog = false
  }

  function showTodoDetails(event) {
    todoItemDetails = {...todoList.find(item => {
      return item.id === event.detail.id
    })}

    displayUpdateDialog = true
  }

  function updateItem(event) {
    const { title, description, done } = event.detail

    const targetIndex = todoList.findIndex(item => {
      return item.id === event.detail.id
    })

    const target = {
      ...todoList[targetIndex],
      title,
      description,
      done
    }

    todoList[targetIndex] = target

    closeUpdateModal()
  }

  function closeUpdateModal() {
    displayUpdateDialog = false
  }
</script>

<style>
  main {
    text-align: center;
    max-width: 240px;
    background: #f6fafd;
  }

  .todo-body {
    width: 100%;
    height: calc(100vh - 18px);
    padding: 50px;
    box-sizing: border-box;
  }

  .todo-items-body {
    width: 100%;
    height: 70%;
    border: 5px solid #BDBDBD;
    border-radius: 20px;
    box-sizing: border-box;
  }

  .todo-button-area {
    display: flex;
    justify-content: center;
    margin-top: 50px;
  }

  .add-button {
    border: none;
    background: #4AC3BF;
    color: white;
    font-size: 3rem;
    width: 200px;
    border-radius: 10px;
    cursor: pointer;
    padding: 0;
    user-select: none;
    box-shadow: 3px 3px 5px 0px #999;
  }

  .add-button:hover {
    opacity: .8;
  }

  .add-button:active {
    box-shadow: none;
    position: relative;
    top: 3px;
    left: 3px;
  }

  .todo-items-list {
    list-style: none;
    padding: 0;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>