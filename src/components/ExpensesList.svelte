<script>
    import SectionTitle from "./Title.svelte";
    import Expense from "./Expense.svelte";
    export let expenses = [];

</script>
<section>
    <SectionTitle title="Expenses List" />
    <ul>
        {#each expenses as expense}
            <Expense {...expense} />
        {:else}
            <h1>There is no expense to show</h1>
        {/each}
    </ul>
</section>