<script>
  import { createEventDispatcher } from "svelte";
  import { blur, fade, fly } from "svelte/transition";
  const dispatch = createEventDispatcher();

  function toggleModal() {
    dispatch("toggle");
    console.log("Triggered from form");
  }
</script>

<style>
  #exit {
    cursor: pointer;
    position: absolute;
    top: 0.5em;
    right: 0.5em;
    z-index: 1001;
  }
</style>

<div
  class="modal-container"
  in:blur={{ duration: 200 }}
  out:fade={{ duration: 200 }}>
  <div class="modal-content" transition:fly={{ y: 200 }}>

    <i
      id="exit"
      class="quaternary-txt far fa-2x fa-times-circle"
      on:click={toggleModal} />

    <slot />
  </div>
</div>
