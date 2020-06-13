<script>
  import expensesData from "../expenses.js";
  import ExpenseList from "./_components/ExpenseList.svelte";
  import ExpenseForm from "./_components/ExpenseForm.svelte";
  import Modal from "./_components/Modal.svelte"
  import { generateUUID } from "../expenses";
  import { setContext, onMount, afterUpdate } from "svelte";

  let expenses = []

  let setName = "";
  let setAmount = null;
  let setId = null;

  let isOpen = false;

  function toggleModal() {
    isOpen = !isOpen;
    setId = null;
    setName = "";
    setAmount = "";
  }

  onMount(()=>{
    expenses = localStorage.getItem('expenses') ?
    JSON.parse(localStorage.getItem('expenses')) : [...expensesData]
  })

  afterUpdate(() => {
    setLocalStorage()
  });

  function setLocalStorage(){
    localStorage.setItem('expenses', JSON.stringify(expenses))
  }

  function clearExpenses() {
    expenses = [];
  }

  function removeExpense(id) {
    expenses = expenses.filter(item => item.id !== id);
    //keep the items that do not have a matching ID
  }
  setContext("remove", removeExpense);

  function addExpense({ name, amount }) {
    let expense = { id: generateUUID(), name, amount };
    expenses = [expense, ...expenses];
  }

  function editExpense({name, amount}){
    expenses = expenses.map(item => {
      return item.id === setId ? {...item, name, amount} : {...item}
    })
    setId = null
    setAmount = null;
    setName = '';
  }

  function setModifiedExpense(id) {
    isOpen = !isOpen;
    let expense = expenses.find(item => item.id === id);
    setId = expense.id;
    setName = expense.name;
    setAmount = expense.amount;
  }
  setContext("modify", setModifiedExpense);
</script>

<div class="container">
  <div class="row d-flex justify-content-center">
  {#if isOpen}
     <Modal on:toggle={ toggleModal }>
      <ExpenseForm on:toggle={ toggleModal }  name={setName} amount={setAmount} {editExpense} {addExpense} {setId} />
    </Modal>
  {/if}
    
    <div class="col-lg-6 col-md-8 col-sm-12" style="max-height:50vh">
      <ExpenseList on:toggle={ toggleModal } {expenses} {clearExpenses} />
    </div>

  </div>

</div>