<script>
    import { json } from 'd3-fetch';
  import { onMount } from 'svelte';
  import Scatter from './Scatterplot.svelte';
  
    let dataset = null;
    let aw = null;
    onMount(async () => {
      aw = await json('/data/gapminder.json');
      dataset = aw.find(d => d.year == '1800').countries
      console.log(dataset)
    });

</script>

{#if dataset}
    <Scatter data={dataset}/>
  {:else}
    <p>Loading...</p>
  {/if}
