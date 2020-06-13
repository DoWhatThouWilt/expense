<script>
  import { createEventDispatcher } from "svelte";
  import { fly } from "svelte/transition";
  import { flip } from "svelte/animate";
  import Expense from "./Expense.svelte";
  export let expenses = [];
  export let clearExpenses;
  import "@smui/list/bare.css";
  import List, {
    Item,
    Text,
    PrimaryText,
    SecondaryText,
    Graphic,
    Meta,
    Label,
    Group,
    Subheader,
    Separator
  } from "@smui/list/bare.js";

  const dispatch = createEventDispatcher();

  function openModal() {
    dispatch("toggle");
    console.log("triggered from ExpenseList");
  }

  $: total = expenses.reduce((acc, curr) => {
    return (acc += curr.amount);
  }, 0);
</script>

<section class="mt-5">
  <div class="card">
    <div class="d-flex justify-content-between">
      <i
        class="mt-3 ml-3 fas fa-2x fa-plus-circle"
        style="visibility:hidden;" />
      <h3 class="secondary-txt card-title mt-3 mb-0">Expense List</h3>
      <i
        class="quaternary-txt mt-3 mr-3 fas fa-2x fa-plus-circle"
        style="cursor:pointer;"
        on:click={openModal} />
    </div>
    <hr />
    <h5 class="tertiary-txt text-center card-title mb-2">
      Total Expenses: ${total}
    </h5>
    <div class="selector">
      <List twoLine>
        <Separator />
        {#each expenses as expense, index (expense.id)}
          <div
            in:fly|local={{ x: 200, delay: (index + 1) * 50 }}
            out:fly|local={{ x: -200 }}
            animate:flip={{duration:350}}>
            <Expense {...expense} />
          </div>
        {/each}
      </List>
    </div>
    <a
      on:click={clearExpenses}
      href="javascript:;"
      class="btn-outline-orange mb-3 btn">
      Clear Expenses
    </a>
  </div>
</section>

<style>
  .selector {
    height: 66vh;
    width: 100%;
    overflow-x: hidden;
    overflow-y: scroll;
    margin: 0 auto;
  }
</style>
