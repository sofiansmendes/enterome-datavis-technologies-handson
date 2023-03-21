<script>
  let current = "";
</script>

<style>
  .selected { 
    background-color: green; 
    }
</style>


<button class="btn btn-secondary" class:selected="{current == 'messi'}" on:click={() => (current = "messi")}>
  Messi
</button>

<button class="btn btn-secondary" class:selected="{current == 'ronaldo'}" on:click={() => (current = "ronaldo")}>
  Ronaldo
</button>

<button class="btn btn-secondary" class:selected="{current == 'neymar'}" on:click={() => (current = "neymar")}>
  Neymar
</button>
