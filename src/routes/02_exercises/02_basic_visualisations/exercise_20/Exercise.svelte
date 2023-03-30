<script>
    // Imports
    import { scaleLinear } from 'd3-scale';
	  import { scaleBand } from 'd3-scale';
	  import { axisBottom } from 'd3-axis';
    import { select } from 'd3-selection';
    import { axisLeft } from 'd3-axis';

    // Dimensions
    const width = 600;
    const height = 300;
    const margin = { top: 10, right: 10, bottom: 30, left: 60 };
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;
  
    // Array
    const data = [
      { service: "Netflix", viewers: 2.9 },
      { service: "Amazon Prime Video", viewers: 1.3 },
      { service: "Disney+", viewers: 2.1 },
      { service: "Hulu", viewers: 0.9 },
      { service: "Apple TV", viewers: 1.1 },
      { service: "Rakuten", viewers: 0.4 }
    ];

    // Scale
    const scaleX = scaleBand().domain(['Netflix','Amazon Prime Video','Disney+','Hulu','Apple TV','Rakuten']).range([0,innerWidth]).paddingInner(0.8).paddingOuter(0.475);
    const scaleY = scaleLinear().domain([0,3]).range([innerHeight,0]);

    // Functions
    function yAxisFunction(element){
    let yAxis = axisLeft(scaleY);
    yAxis(select(element));
  }
  function xAxisFunction(element){
    let xAxis = axisBottom(scaleX);
    xAxis(select(element));
  }

  </script>
  
  <!-- setting a viewBox and max-width allows the SVG to shrink but not grow! -->
  <svg viewbox="0 0 {width} {height}" style="max-width: {width}px">
    <text x=0 y=0 transform=" translate(30,180) rotate(270)">Viewers (Million)</text>
    <g transform={`translate(${margin.left},${margin.top})`}>
      {#each data as d}
        <rect x={scaleX(d.service)-25} y={scaleY(d.viewers)} width=70 
        height={innerHeight-scaleY(d.viewers)}/>
      {/each}
    </g>
    <g transform="translate({margin.left},{margin.top})" use:yAxisFunction>
    </g>
    <g transform="translate({margin.left},{innerHeight+margin.top})" use:xAxisFunction>
    </g>  
  </svg>
  
  <style>
    rect { 
      fill: rgb(88, 189, 88); 
      stroke: black;
    }
    text {
		fill: currentColor;
		font-size: 0.65em;
	  }
  </style>