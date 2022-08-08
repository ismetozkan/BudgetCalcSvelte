<script>
    import {setContext, onMount, afterUpdate} from 'svelte';

    // Components
    import Navbar from "./components/Navbar.svelte";
    import ExpensesList from "./components/ExpensesList.svelte";
    import Total from "./components/Total.svelte";
    import AddExpense from "./components/AddExpense.svelte";
    // Data
    //import expensesData from "./expenses.js";
    //let expenses = [...expensesData];

    // Variables
    let expenses = [];
    let isFormOpen = false;

    //Editing Variables
    let setId = null;
    let setName = '';
    let setAmount = null;
    $: isEditing = !!setId;


    console.log({expenses});
        // sum values instantly
    $: total = expenses.reduce((preVal, currVal) =>
            preVal + currVal.amount, 0);

    // Functions
    function showForm(){
       isFormOpen = true;
    }
    function hideForm(){
       isFormOpen = false;
       setId = null;
       setName = '';
       setAmount = null;
    }

    function addExpense({name, amount}) {
        let newExpense = {
        id: Math.random() * Date.now(),
        name: name,
        amount: amount
        };
        expenses = [newExpense,...expenses];
    }

    function setModExpense(id){
        let expense = expenses.find(item => item.id === id);
        setId = expense.id;
        setName = expense.name;
        setAmount = expense.amount;
        showForm();
    }

    function editExpense({name, amount}){
        expenses = expenses.map(item => {
            return item.id === setId
                ? {...item,
                    name: name,
                    amount: amount}
                : {...item};

        });
        setId = null;
        setName = '';
        setAmount = null;
    }

    function removeExpense(id){
        expenses = expenses.filter(item => item.id !== id)
    }

    function clearExpenses(){
        expenses = [];
        // todo: ADD PRESS & HOLD TO CLEAR EXPENSE BUTTON
    }
    // Context
    setContext('remove',removeExpense )
    setContext('modify',setModExpense )

    //Local Storage
    function setLocalStorage() {
        localStorage.setItem('expenses',JSON.stringify(expenses));
    }
            //lifecycle functions
    onMount(() => {
       expenses = localStorage.getItem('expenses')
        ? JSON.parse(localStorage.getItem('expenses'))
        : [];
    });
    afterUpdate(() => {
        console.log('updated');
        setLocalStorage();
    });

</script>
<Navbar {showForm} />
<main class="content">
    {#if isFormOpen}
    <AddExpense {addExpense} name={setName} amount={setAmount}
                {isEditing} {editExpense} {hideForm}/>
    {/if}

    <Total title="Total Expenses" { total }/>
    <ExpensesList {expenses} />

    <button type="button" class="btn btn-primary btn-block"
            on:click = {clearExpenses}>
        Clear Expenses
    </button>
</main>



