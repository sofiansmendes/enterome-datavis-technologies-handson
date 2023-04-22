<script>
  // Properties
  export let data = [];
  export let year = 0; //1800
  export let cont_dropdown = "all";  

  const continents = ["europe", "asia", "americas", "africa"];
  let timer = false;
  let clicked = false; 

  function year_increment() { 
    if (year == 214) { //at the end needs to jump back to 1800 (213 observations) 
      year = 0;
    } else {
      year += 1;
    }
  }

  function start_stop() {
    if (timer == false) {
      timer = setInterval(year_increment, 100); //starting
      clicked = true;
    } else {
      clearInterval(timer); //stopping
      timer = false;
      clicked = false; 
    }
  } 

  function reset() {
    clearInterval(timer);
    timer = false;
    year = 0;
    clicked = false; 
  } 

</script>

<div class="row">
  <div>
    {#if clicked == false}
      <button class="btn btn-success" on:click={start_stop}>Start</button>
    {:else}
      <button class="btn btn-danger" on:click={start_stop}>Stop</button>
    {/if}
      <button class="btn btn-secondary" on:click={reset}>Reset</button>
  </div>
  <div>
    <label for="slider">Year: {1800 + year}</label>
    <input type="range" class="form-range" min="0" max="214" bind:value={year} id="slider">
  </div> 
  <div> 
    <select class="btn btn-primary dropdown-toggle" data-toggle="dropdown" bind:value={cont_dropdown}>
      <option value="all">All continents</option>
      <option value="europe">Europe</option>
      <option value="asia">Asia</option>
      <option value="americas">North- and South-America</option>
      <option value="africa">Africa</option>
    </select> 
  </div>

</div>
