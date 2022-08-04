<script>
    import SectionTitle from "./Title.svelte";
    import Expense from "./Expense.svelte";
    export let expenses = [];
    export let removeExpense;

</script>
<section>
    <SectionTitle title="Expenses List" />
    <ul>
        {#each expenses as expense, index}
            <Expense {...expense} {removeExpense} />
        {:else}
            <h1>There is no data</h1>
        {/each}
    </ul>
</section>
