<Modal height={ '40vh' } title={ '更新' } on:closeModal={ closeModal }>
  <table class="update-form-table">
    <tr>
      <th>
        名前
      </th>
      <td>
        <input
          class="update-title"
          type="text"
          bind:value={ todoItemDetails.title }
        >
      </td>
    </tr>
    <tr>
      <th>
        状態
      </th>
      <td>
        <input
          class="update-done"
          type="checkbox"
          id="done"
          bind:checked={ todoItemDetails.done }
        >
        <label for="done">
          完了
        </label>
      </td>
    </tr>
    <tr>
      <th>
        説明
      </th>
      <td>
        <textarea class="update-description" cols="30" rows="10" bind:value={ todoItemDetails.description }></textarea>
      </td>
    </tr>
  </table>
  <div class="update-dialog-buttons">
    <button class="update-button" on:click={ update }>
      決定
    </button>
    <button class="cancel-button" on:click={ closeModal }>
      キャンセル
    </button>
  </div>
</Modal>

<script>
  import { createEventDispatcher } from 'svelte'
  import Modal from './modalBase.svelte'

  export let todoItemDetails = {}

  const dispatch = createEventDispatcher()

  function update() {
    dispatch('update', todoItemDetails)
  }

  function closeModal() {
    dispatch('closeModal')
  }
</script>

<style>
  .update-form-table {
    width: 80%;
    margin:auto;
    border-spacing: 0 15px;
  }

  .update-form-table > tr {
    text-align: left;
  }

  .update-title,
  .update-description {
    width: 100%;
    box-sizing: border-box;
  }

  .update-button,
  .cancel-button {
    width: 135px;
    height: 40px;
    font-size: 1.5rem;
    border: none;
    border-radius: 5px;
    color: white;
    cursor: pointer;
    box-shadow: 3px 3px 5px 0px #999;
  }

  .update-button {
    background: #4AC3BF;
  }

  .cancel-button {
    background: #c34a4e;
  }

  .update-button:hover,
  .cancel-button:hover {
    opacity: .8;
  }

  .update-button:active,
  .cancel-button:active {
    box-shadow: none;
    position: relative;
    top: 3px;
    left: 3px;
  }

  .update-dialog-buttons {
    margin-top: 10px;
  }
</style>