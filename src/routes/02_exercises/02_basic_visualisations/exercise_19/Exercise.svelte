<script>
    // Imports
		import {scaleLinear,scaleOrdinal} from 'd3-scale';
		import {schemeDark2} from 'd3-scale-chromatic';

    // Dimensions
    const width = 800;
    const height = 100;
    const margin = { top: 20, right: 5, bottom: 5, left: 5 };
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;
  
    // Array
    const values = [
      { x: 2, y: 1, category: "cat1" },
      { x: 4, y: 2, category: "cat3" },
      { x: 6, y: 1, category: "cat2" },
      { x: 7, y: 3, category: "cat3" },
      { x: 9, y: 1, category: "cat2" }
    ];

    // Scales
		const scaleX = scaleLinear().domain([1,10]).range([0,innerWidth]);
		const scaleY = scaleLinear().domain([1,3]).range([innerHeight,0]);
		const scaleCol = scaleOrdinal(schemeDark2);
  </script>
  
  <svg viewBox="0 0 {width} {height}">
    <g transform="translate({margin.left},{margin.top})">
      {#each values as val}
				<circle cx={scaleX(val.x)} cy={scaleY(val.y)} r="5" style={"fill:" + scaleCol(val.category)}/>
				<text class=valueLabel x={scaleX(val.x)} y={scaleY(val.y)-10}> {val.y} </text>
				<line x1={scaleX(val.x)} y1={scaleY(val.y)} x2={scaleX(val.x)} y2={innerHeight} /> 
			{/each}
    </g>
  </svg>
  
  <style>
    line {
    stroke: black;
    }
    text {
      text-anchor: middle;
      font-size: small;
    }
  </style>
  