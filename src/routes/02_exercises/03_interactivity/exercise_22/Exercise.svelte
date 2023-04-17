<script>
    let count = 0;

function handleClick(event) {
    count += 1;
}

function resetClick(event) {
    count = 0;
}
</script>

<button class="btn btn-info" on:click={handleClick}> Count: {count} </button>
<button class="btn btn-warning" on:click={resetClick}> Reset </button>