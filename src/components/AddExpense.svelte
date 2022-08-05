<script>
    import Title from "./Title.svelte";
</script>
<section class="form">
    <Title title="Add Expense"/>
    <form action="" class="expense-form">
        <div class="form-control">
            <label for="name">Name</label>
            <input type="text" id="name">
            <label for="amount">Amount</label>
            <input type="number" id="amount">
        </div>
        <p class="form-empty">Fill It to Add Expense</p>
        <button type="submit" class="btn btn-block">Add Expense</button>
        <button type="button" class="close-btn">
            <i class="fas fa-times-circle"></i>
            Close
        </button>
    </form>
</section>