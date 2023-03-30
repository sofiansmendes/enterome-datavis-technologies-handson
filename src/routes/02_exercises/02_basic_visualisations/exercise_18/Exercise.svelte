<script>
    // Imports
    import { scaleLog } from 'd3-scale';
    import { axisBottom } from 'd3-axis';
    import { select } from 'd3-selection';

    // Dimensions
    const width = 800;
    const height = 100;
    const margin = { top: 5, right: 5, bottom: 25, left: 5 };
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;
  
    // Array
    const values = [2, 4, 6, 7, 9];

    // Scale
    const scale = scaleLog().domain([1,10]).range([0,innerWidth]);

    // Function
    function axisFunction(element){
    const xAxis = axisBottom(scale);
    xAxis(select(element));
    }
  </script>
  
  <svg viewBox="0 0 {width} {height}">
    <g transform="translate({margin.left},{margin.top})">
    {#each values as val}
      <circle cx={scale(val)} cy={innerHeight/2} r="10"/>
    {/each}
    <text x={innerWidth/2} y={height-margin.top}> x axis </text> 
    </g>
    <g transform="translate({margin.left},{innerHeight})" use:axisFunction>
    </g>
  </svg>
  
  <style>
    circle {
      fill: steelblue;
    }
    text {
      fill: currentColor;
      font-size: 0.67em;
    }
  </style>