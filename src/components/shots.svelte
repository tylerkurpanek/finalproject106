<script>
    import { onMount } from 'svelte';
    import * as d3 from 'd3';
  
  
    let svg;
    let container;
    let shotData;

    //const resShot = await fetch('lebron_shots_with_year.csv');
    //const csvShot = await resLebron.text();
    //shotData = d3.csvParse(csvLebron, d3.autoType);
    
  
    onMount(() => {

      async() => {
        shotData = d3.csv("lebron_shots_with_year.csv")
      }
      
      //const resShot = await fetch('lebron_shots_with_year.csv');
      //const csvShot = await resLebron.text();
      //shotData = d3.csvParse(csvLebron, d3.autoType);

      const margin = { top: 20, right: 20, bottom: 20, left: 20 };
      const width = window.innerWidth - margin.left - margin.right;
      const height = window.innerHeight - margin.top - margin.bottom;
  
      const svgContainer = d3.select(svg)
        .attr("width", width)
        .attr("height", height);
  
      const g = svgContainer.append("g")
        .attr("transform", `translate(${margin.left},${margin.top})`);

      console.log(width)
      var svg = d3.select("#my_dataviz")
.append("svg")
  .attr("width", width + margin.left + margin.right)
  .attr("height", height + margin.top + margin.bottom)
.append("g")
  .attr("transform",
        "translate(" + margin.left + "," + margin.top + ")");

$: console.log(shotData)

// Labels of row and columns
var myGroups = ["A", "B", "C", "D", "E", "F", "G", "H", "I", "J"]
var myVars = ["v1", "v2", "v3", "v4", "v5", "v6", "v7", "v8", "v9", "v10"]

// Build X scales and axis:
var x = d3.scaleBand()
  .range([ 0, width ])
  .domain(myGroups)
  .padding(0.01);
svg.append("g")
  .attr("transform", "translate(0," + height + ")")
  .call(d3.axisBottom(x))

// Build X scales and axis:
var y = d3.scaleBand()
  .range([ height, 0 ])
  .domain(myVars)
  .padding(0.01);
svg.append("g")
  .call(d3.axisLeft(y));

// Build color scale
var myColor = d3.scaleLinear()
  .range(["white", "#69b3a2"])
  .domain([1,100])

//Read the data
d3.csv("https://raw.githubusercontent.com/holtzy/D3-graph-gallery/master/DATA/heatmap_data.csv", function(data) {

  svg.selectAll()
      .data(data, function(d) {return d.group+':'+d.variable;})
      .enter()
      .append("rect")
      .attr("x", function(d) { return x(d.group) })
      .attr("y", function(d) { return y(d.variable) })
      .attr("width", x.bandwidth() )
      .attr("height", y.bandwidth() )
      .style("fill", function(d) { return myColor(d.value)} )

})

      

  });
    

  </script>
  <div class="g" bind:this={container} />

  <style>
    .g {
      width: 100%;
      height: 100vh; /* check problem when setting width */
      position: absolute;
      transition: opacity 2s, visibility 2s;
      outline: blue solid 3px;
    }
  
    
  </style>
  
  <svg bind:this={svg}></svg>