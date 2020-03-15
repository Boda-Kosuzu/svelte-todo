<Modal height={ '40vh' } title={ '登録' } on:closeModal={ closeModal }>
  <table class="register-form-table">
    <tr>
      <th>
        名前
      </th>
      <td>
        <input
          class="register-title"
          type="text"
          bind:value={ title }
        >
      </td>
    </tr>
    <tr>
      <th>
        説明
      </th>
      <td>
        <textarea class="register-description" rows="10" bind:value={ description }></textarea>
      </td>
    </tr>
  </table>
  <div class="register-dialog-buttons">
    <button class="register-button" on:click={ register }>
      登録
    </button>
    <button class="cancel-button" on:click={ closeModal }>
      キャンセル
    </button>
  </div>
</Modal>

<script>
  import { createEventDispatcher } from 'svelte'
  import Modal from './modalBase.svelte'

  const dispatch = createEventDispatcher()

  let title = ''
  let description = ''

  function register() {
    dispatch('register', {title, description})
  }

  function closeModal() {
    dispatch('closeModal')
  }
</script>

<style>
  .register-form-table {
    width: 80%;
    margin:auto;
    border-spacing: 0 15px;
  }

  .register-form-table > tr {
    text-align: left;
  }

  .register-title,
  .register-description {
    width: 100%;
    box-sizing: border-box;
  }

  .register-button,
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

  .register-button {
    background: #4AC3BF;
  }

  .cancel-button {
    background: #c34a4e;
  }

  .register-button:hover,
  .cancel-button:hover {
    opacity: .8;
  }

  .register-button:active,
  .cancel-button:active {
    box-shadow: none;
    position: relative;
    top: 3px;
    left: 3px;
  }

  .register-dialog-buttons {
    margin-top: 10px;
  }
</style>