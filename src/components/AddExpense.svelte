<script>
    import Title from "./Title.svelte";
    let name = '';
    let amount = null;
    export let addExpense;
    //$: console.log({name, amount});
    $: isEmpty = !name || !amount;
    function handleSubmit(){
        addExpense({name, amount})
        name = '';
        amount = null;
    }

</script>
<section class="form">
    <Title title="Add Expense"/>
    <form action="" class="expense-form" on:submit|preventDefault={handleSubmit}>
        <div class="form-control">
            <label for="name">Name</label>
            <input type="text" id="name" bind:value= {name}>
            <label for="amount">Amount</label>
            <input type="number" id="amount" bind:value= {amount}>
        </div>
        {#if isEmpty}
        <p class="form-empty">Fill It to Add Expense</p>
        {/if}
        <button type="submit" class="btn btn-block"
                class:disabled={isEmpty}
                disabled= { isEmpty }>
            Add Expense
        </button>
        <button type="button" class="close-btn">
            <i class="fas fa-times-circle"></i>
            Close
        </button>
    </form>
</section>