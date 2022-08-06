<script>
    import {setContext} from 'svelte';

    // Components
	import Navbar from "./components/Navbar.svelte";
    import ExpensesList from "./components/ExpensesList.svelte";
    import Total from "./components/Total.svelte";
    import AddExpense from "./components/AddExpense.svelte";
    // Data
    import expensesData from "./expenses.js";

    // Variables
    let expenses = [...expensesData];
    console.log(expenses);
        // sum values instantly
    $: total = expenses.reduce((preVal, currVal) =>
            preVal + currVal.amount, 0);

    // Functions
    function addExpense({name, amount}) {
        let newExpense = {
        id: Math.random() * Date.now(),
        name: name,
        amount: amount
        };
        expenses = [newExpense,...expenses];
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
</script>
<Navbar />
<main class="content">
    <AddExpense {addExpense}/>
    <Total title="Total Expenses" { total }/>
    <ExpensesList {expenses} />

    <button type="button" class="btn btn-primary btn-block"
            on:click = {clearExpenses}>
        Clear Expenses
    </button>
</main>



