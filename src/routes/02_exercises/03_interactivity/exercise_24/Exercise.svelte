<script>
  import { json } from "d3-fetch";
  import { onMount } from "svelte";

  import Controls from "./Controls.svelte";
  import Scatterplot from "./Scatterplot.svelte";

  // Load the data
  let data = null;
  onMount(async () => {
    data = await json("/data/gapminder.json");
  });

  let year = 0;
  let cont = "all"; 
  const continents = ["europe", "asia", "americas", "africa"];

  function select_data(year, location) {
    let data_2 = data[year]['countries'];
    if (continents.includes(location)) {
      return data_2.filter(d => d.continent == location);
    } else {
      return data_2;
    }
  }

</script>

{#if !data}
  <p>Loading the data, please wait...</p>
{:else}
  <div>
    <Scatterplot data={select_data(year, cont)} />
    <Controls data={data} bind:year={year} bind:cont_dropdown={cont} />
  </div>
{/if}
