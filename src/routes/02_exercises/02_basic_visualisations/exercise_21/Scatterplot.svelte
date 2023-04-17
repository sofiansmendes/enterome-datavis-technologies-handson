<script>
    // Dimensions
    const [height, width] = [400, 600];
    const margin = { top: 50, right: 5, bottom: 55, left: 50 };
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;

      // Importing
  import {scaleLinear} from "d3-scale";
  import {scaleOrdinal} from "d3-scale";
  import {scaleLog} from 'd3-scale';
  import {scaleSqrt} from 'd3-scale';
  import {extent} from 'd3-array';
  import {axisLeft} from 'd3-axis';
  import {axisBottom} from 'd3-axis';
  import {select} from 'd3-selection';
  import {schemeTableau10} from 'd3-scale-chromatic';

  export let data;
  const xScale = scaleLog().domain([300,100000]).range([0, innerWidth]);
  const yScale = scaleLinear().domain([0,90]).range([innerHeight, 0]);
  const color = scaleOrdinal(schemeTableau10).domain(extent(data.map(function(dat){return dat.continent;})));
  const radius = scaleSqrt().domain([0,5e8]).range([5,10]);
  const ticks = [400,4000,40000];
  const tickLabels = ["$400", "$4000", "$40000"]
  function xAxis(x) {axisBottom(xScale).tickValues(ticks).tickFormat((d,i) => tickLabels[i])(select(x))};
  function yAxis(x) {axisLeft(yScale)(select(x))};

  </script>
  
  <svg viewBox="0 0 {width} {height}" style="max-width: {width}px">
    <text x=0 y=0 transform="translate(20,265) rotate(270)" fill="currentColor" font-size=1.2em>Life Expectancy</text>
    <g transform="translate({margin.left}, {margin.top})">
      {#each data as dat}
    {#if dat.income !== null && dat.life_exp !== null && dat.population !== null}
      <circle cx={xScale(+dat.income)} cy={yScale(+dat.life_exp)} r={radius(+dat.population)} fill={color(dat.continent)} opacity=0.8/>
    {/if}
    {/each}
    <text x={innerWidth/2} y=0 text-anchor="middle" font-size=2.25em> Gapminder Scatterplot</text>
    <text x={innerWidth/2} y={innerHeight+40} text-anchor="middle" fill="currentColor" font-size=1.2em> GDP per Capita </text>
    <text x={innerWidth-80} y={innerHeight-10} text-anchor="left" fill="currentColor" font-size=2.2em opacity=0.5> 1800 </text>

    </g>
    <g use:xAxis transform="translate({margin.left},{innerHeight+margin.top})">
    </g>
    <g use:yAxis transform="translate({margin.left},{margin.top})">
    </g>
  
  </svg>
  