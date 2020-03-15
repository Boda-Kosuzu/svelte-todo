<div transition:fade={ {delay: 0, duration: 200} }>
  <div class="modal-background">
    <div 
      class="modal-body"
      style={ `width: ${width}; height: ${height}` }
    >
      <div class="modal-header">
        <div class="modal-header-left">
         { title }
        </div>
        <div class="modal-header-right">
          <div
            class="modal-close-icon"
            on:click={ close }
          >
            <Icon { icon } />
          </div>
        </div>
      </div>
      <div class="modal-contents">
        <slot></slot>
      </div>
    </div>
  </div>
</div>
<svelte:window on:keydown={ closeEsc } />

<script>
  import { createEventDispatcher } from 'svelte'
  import { fade } from 'svelte/transition'
  import Icon from 'fa-svelte'
  import { faTimes } from '@fortawesome/free-solid-svg-icons/faTimes'

  export let width = '30vw'
  export let height = '80vh'
  export let title = ''
  // export let closeButton = true
  // export let closeOnEsc = true
  // export let closeOnOuterClick = true
  // export let styleBg = { top: 0, left: 0 }
  // export let styleWindow = {}
  // export let styleContent = {}
  // export let setContext = baseSetContext
  // export let transitionBg = fade
  // export let transitionBgProps = { duration: 250 }
  // export let transitionWindow = transitionBg
  // export let transitionWindowProps = transitionBgProps

  const icon = faTimes
  const dispatch = createEventDispatcher()

  function closeEsc(event){
    if(event.key === 'Escape') close()
  }

  function close () {
    dispatch('closeModal')
  }

</script>

<style>
.modal-background {
  background: rgba(0, 0, 0, 0.5);
  position: absolute;
  width: 100vw;
  height: 100vh;
  top: 0;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal-body {
  background: #f6fafd;
  border-radius: 3px;
  overflow: hidden;
  box-shadow: 5px 5px 5px 5px rgba(0, 0, 0, .2);
}

.modal-header {
  width: 100%;
  display: flex;
  justify-content: space-between;
  padding: 5px;
  padding-bottom: 0 !important;
  box-sizing: border-box;
}

.modal-close-icon {
  color: #adb4b9;
  cursor: pointer;
  display: flex;
}

.modal-contents {
  padding: 10px;
}
</style>