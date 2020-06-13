<script>
  export let name = "";
  export let amount = null;
  export let setId = null;
  export let addExpense;
  export let editExpense;

  import { createEventDispatcher } from 'svelte'
  const dispatch = createEventDispatcher()

  $: isEmpty = !name || !amount;

  function toggleModal() {
    dispatch('toggle')
    console.log("Triggered from form submission")
  }

  function handleSubmit() {
    if (setId) {
      editExpense({ amount, name });
    } else {
      addExpense({ amount, name });
    }
    name = "";
    amount = null;
    toggleModal();
  }
</script>

<style>
  .hidden {
    visibility: hidden;
  }
  .md-form label {
    font-size: 0.8em;
    margin-top: -0.7em;
  }
  .field {
    display: flex;
    flex-flow: column-reverse;
  }
  label {
    z-index: 0;
  }
  label,
  input {
    transition: all 0.2s;
    touch-action: manipulation;
  }

  input {
    z-index: 2;
    margin-top: 1em;
    font-size: 1.25em;
    border: 0;
    border-bottom: 1px solid #ddd;
    font-family: inherit;
    -webkit-appearance: none;
    border-radius: 0;
    padding: 0;
    cursor: text;
  }

  input:focus {
    outline: 0;
    border-bottom: 1px solid #666;
  }
  input:placeholder-shown + label {
    cursor: text;
    max-width: 66.66%;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    transform-origin: left bottom;
    transform: translate(0, 2.125rem) scale(1.5);
  }
  ::-webkit-input-placeholder {
    opacity: 0;
    transition: inherit;
  }
  input:focus::-webkit-input-placeholder {
    opacity: 0;
  }
  input:not(:placeholder-shown) + label,
  input:focus + label {
    transform: translate(0, 0) scale(1);
    cursor: pointer;
  }
</style>

<div class="card">
    <h3 class="secondary-txt text-center card-title mt-3 mb-0">
      {setId ? 'Editing' : 'Add New Expense'}
    </h3>
  <hr />
  <!--Card content-->
  <div class="card-body px-lg-5 pt-0">

    <!-- Form -->
    <form
      class="text-center"
      style="color: #757575;"
      on:submit|preventDefault={handleSubmit}>

      <div class="md-form field">
        <input
          bind:value={name}
          placeholder="Name"
          type="text"
          class="form-control" />
        <label for="name">Name</label>
      </div>

      <div class="md-form field">
        <input
          onkeydown="return event.keyCode !== 69"
          bind:value={amount}
          placeholder="Amount"
          type="number"
          class="form-control" />
        <label for="amount">Amount</label>
      </div>

      <p class="quaternary-txt hidden" class:hidden={!isEmpty}>
        Please fill out all the fields.
      </p>

      <button
        disabled={isEmpty}
        type="submit"
        class="btn btn-outline-orange btn-block my-4 ripple">
        {setId ? "Edit Expense" : "Add Expense"}
      </button>

    </form>
    <!-- Form -->

  </div>

</div>
