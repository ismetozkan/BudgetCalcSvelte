<script>
    import SectionTitle from "./Title.svelte";
    import Expense from "./Expense.svelte";
    export let expenses = [];
</script>
<section>
    <SectionTitle title="Expenses List" />
    <ul>
        {#each expenses as expense}
            <Expense  />
        {/each}
    </ul>
</section>
