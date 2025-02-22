<script>
  import { extent } from "d3-array";
  import { select } from "d3-selection";
  import { scaleLinear } from "d3-scale";
  import { axisBottom, axisLeft } from "d3-axis";
  import { brush } from "d3-brush";

  // Properties
  export let data = [];
  export let x = (d) => d.x;
  export let y = (d) => d.y;
  export let xLabel = "x";
  export let yLabel = "y";
  export let selected_both = [];
  export let selected_local = [];


  // Dimensions
  const width = 300;
  const height = 230;
  const margin = { top: 10, right: 10, bottom: 35, left: 45 };
  const innerWidth = width - margin.left - margin.right;
  const innerHeight = height - margin.top - margin.bottom;

  // Scales
  const xScale = scaleLinear().domain(extent(data, x)).range([0, innerWidth]);
  const yScale = scaleLinear().domain(extent(data, y)).range([innerHeight, 0]);

  // Axes
  const xAxis = (node) => axisBottom(xScale)(select(node));
  const yAxis = (node) => axisLeft(yScale)(select(node));

  // Brushing
  // The range of the selection rectangle.
  // If there is no active selection, it contains: null,
  // otherwise, it contains: [ [x0, y0], [x1, y1] ]
  let range = null;
  const my_brush = (node) => brush().on('start', brush_function).on('brush', brush_function).on('end', brush_function)(select(node));
  let coords = [];

  for (let i = 0; i < data.length; i++) {
    coords[i] = [xScale(x(data[i])), yScale(y(data[i]))];
  }

  if (range == null) {
    for (let i = 0; i < data.length; i++) {
      selected_local[i] = true; //all datapoints set to true if no active selection
    }
  }

  function brush_function({selection}) {
    if (selection) {
      range = selection;
      for (let i = 0; i < data.length; i++) {
        if (range != null && coords[i][0] >= range[0][0] && coords[i][0] <= range[1][0] && coords[i][1] >= range[0][1] && coords[i][1] <= range[1][1]) {
          selected_local[i] = true;
        } else {
          if (range != null) {
            selected_local[i] = false;
          } else {
            selected_local[i] = true;
          }
        }
      }
    }
  }

</script>

<svg viewBox="0 0 {width} {height}" class="mx-2" style="max-width: {width}px">
  <g transform="translate({margin.left},{margin.top})" use:my_brush>
    <g>
      {#each data as d,idx}
        <circle
        class="selected"
        class:unselected={selected_both[idx] == false}
        cx={coords[idx][0]}
        cy={coords[idx][1]}
        r={3}
        />
      {/each}
    </g>
    <g use:xAxis transform="translate(0, {innerHeight})">
      <text class="axisLabel" x={innerWidth / 2} y={margin.bottom - 5}
        >{xLabel}</text
      >
    </g>
    <g use:yAxis>
      <text
        class="axisLabel"
        y={-margin.left + 10}
        x={-innerHeight / 2}
        transform="rotate(-90)">{yLabel}</text
      >
    </g>
  </g>
</svg>

<style>
  .axisLabel {
    text-anchor: middle;
    vertical-align: bottom;
    fill: currentcolor;
  }
  .selected {
    fill: steelblue;
    fill-opacity: 0.5;
    stroke: steelblue;
    stroke-opacity: 1;
    stroke-width: 1.5;
  }
  .unselected {
    fill: darkgray;
    fill-opacity: 0.3;
    stroke: darkgray;
    stroke-opacity: 0.5;
    stroke-width: 1.5;
  }

</style>
