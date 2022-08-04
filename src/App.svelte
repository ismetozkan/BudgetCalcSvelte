<script>
    // Components
	import Navbar from "./components/Navbar.svelte";
    import ExpensesList from "./components/ExpensesList.svelte";

    // Data
    import expensesData from "./expenses.js";

    // Variables
    let expenses = [...expensesData];
    console.log(expenses);

    // Functions

</script>
<Navbar />
<main class="content">
    <ExpensesList {expenses} />
</main>




