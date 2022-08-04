<script>
    import {setContext} from 'svelte';

    // Components
	import Navbar from "./components/Navbar.svelte";
    import ExpensesList from "./components/ExpensesList.svelte";

    // Data
    import expensesData from "./expenses.js";

    // Variables
    let expenses = [...expensesData];
    console.log(expenses);

    // Functions
    function removeExpense(id){
        expenses = expenses.filter(item => item.id !== id)
    }
    setContext('remove',removeExpense )

</script>
<Navbar />
<main class="content">
    <ExpensesList {expenses} />
</main>




