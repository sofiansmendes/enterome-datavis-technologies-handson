<script>
  import { csv } from "d3-fetch";
  import { onMount } from "svelte";
  import Scatter from "./Scatterplot.svelte";

  // Load the data
  let data = null;
  onMount(async () => {
    data = await csv("/data/cars-2.csv");
  });

  // Configurations
  const s1 = {
    x: (d) => +d.Horsepower,
    y: (d) => +d.Acceleration,
    xLabel: "Horsepower",
    yLabel: "Acceleration",
  };
  const s2 = {
    x: (d) => +d.Displacement,
    y: (d) => +d.Miles_per_Gallon,
    xLabel: "Displacement",
    yLabel: "Miles per Gallon",
  };

  $: selected_1 = [];
  $: selected_2 = [];
  $: selected_both = combine_both(selected_1, selected_2);
  let result = [];

  function combine_both(sp1, sp2) {
    for (let i = 0; i < 406; i++) {
      if (sp1[i] == true & sp2[i] == true) {
        result[i] = true;
      } else {
        result[i] = false;
      }
    }
    return result;
  }
</script>

{#if !data}
  <p>Loading the data, please wait...</p>
{:else}
  <div class="d-flex justify-content-around">
    <Scatter {data} {...s1} {selected_both} bind:selected_local={selected_1}/>
    <Scatter {data} {...s2} {selected_both} bind:selected_local={selected_2}/>
  </div>
{/if}
