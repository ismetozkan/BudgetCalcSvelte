<script>
    import {getContext} from 'svelte';
    export let id;
    export let name='';
    export let amount = 0;

    let displayAmount = false;
    function toggleAmount() {
        displayAmount = !displayAmount
    }
    const removeExpense = getContext('remove');
    const setModExpense = getContext('modify');

</script>

<article class="single-expense">
    <div class="expense-info">
        <h2>{name}
            <button class="amount-btn" on:click = {toggleAmount}>
                {#if !displayAmount}
                <i class="fas fa-caret-down"></i>
                {:else}
                <i class="fas fa-caret-up"></i>
                {/if}
            </button>
        </h2>
            {#if displayAmount}
                <h4>Amount: {amount}</h4>
            {/if}
    </div>
    <div class="expense-buttons">
        <button class="expense-btn edit-btn" on:click = {setModExpense(id)}>
            <i class="fas fa-pen"></i>
        </button>
        <button class="expense-btn delete-btn" on:click = {removeExpense(id)}>
            <i class="fas fa-trash"></i>
        </button>
    </div>
</article>