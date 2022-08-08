<script>
    import Title from "./Title.svelte"

    //import {onMount, onDestroy, beforeUpdate, afterUpdate} from 'svelte';
    //onMount(() => {
    //    console.log('the component has mounted');
    //});
    //onDestroy(() => {
    //    console.log('the component has destroyed');
    //});

    export let name = '';
    export let amount = null;
    export let addExpense;
    export let isEditing;
    export let editExpense;
    export let hideForm;
    //$: console.log({name, amount});
    $: isEmpty = !name || !amount;

    function handleSubmit(){
        if(isEditing){
            editExpense({name, amount})
        }else {
            addExpense({name, amount})
        }
        name = '';
        amount = null;
    }

</script>
<section class="form">
    {#if isEditing}<Title title="Edit Expense"/>
    {:else}<Title title="Add Expense"/>
    {/if}
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
            {#if isEditing}Edit Expense
            {:else}Add Expense
            {/if}

        </button>
        <button type="button" class="close-btn" on:click={hideForm}>
            <i class="fas fa-times-circle"></i>
            Close
        </button>
    </form>
</section>