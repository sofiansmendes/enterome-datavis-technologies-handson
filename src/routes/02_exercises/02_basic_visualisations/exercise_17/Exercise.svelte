<script>
    // Dimensions
    const width = 800;
    const height = 100;
    const margin = { top: 5, right: 5, bottom: 5, left: 5 };
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;
  
    // Array
    const values = [2, 4, 6, 7, 9];

    // Scale
    import { scaleLog } from 'd3-scale';
    const scale = scaleLog().domain([1,10]).range([0,innerWidth]);
  </script>
  
  <svg viewBox="0 0 {width} {height}">
    <g transform="translate({margin.left},{margin.top})">
    {#each values as val}
      <circle cx={scale(val)} cy={innerHeight/2} r="10"/>
    {/each}
    </g>
  </svg>
  