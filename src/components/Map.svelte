<script>
    import { onMount } from 'svelte';
    import * as d3 from 'd3';
    //export let index;
    let shotData;
  
  
    let svg;
    let container;

    //const resShot = await fetch('lebron_shots_with_year.csv');
    //const csvShot = await resLebron.text();
    //shotData = d3.csvParse(csvLebron, d3.autoType);
    
  
    onMount(() => {
      //async() => {
      //  shotData = await d3.csv("lebron_shots_with_year.csv")
      //}
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
      // Top left corner of court is 600,40
      // dimensions are multiplied by 10 
      // middle of the court is 850
      //Hoop
      console.log(width)
      //rim
      g.append("circle")
        .attr("cx", width/2) 
        .attr("cy",92.5 ) 
        .attr("r", 7.5) 
        .attr('fill', 'none')
        .attr('stroke', 'black')
    //baseline
     g.append('rect')
        .attr('x', (width/2)-250)
        .attr('y', 40)
        .attr('width', 250)
        .attr('height', 1)
        .attr('fill', 'none')
        .attr('stroke', 'black')

      g.append('rect')
        .attr('x', (width/2))
        .attr('y', 40)
        .attr('width', 250)
        .attr('height', 1)
        .attr('fill', 'none')
        .attr('stroke', 'black')
    //left sideline
    g.append('rect')
        .attr('x', (width/2) + 250)
        .attr('y', 40)
        .attr('width', 1)
        .attr('height',470 )
        .attr('fill', 'none')
        .attr('stroke', 'black')
    //right sideline
    g.append('rect')
        .attr('x', (width/2) - 250)
        .attr('y', 40)
        .attr('width', 1)
        .attr('height',470 )
        .attr('fill', 'none')
        .attr('stroke', 'black')
    //halfcourt line 
    g.append('rect')
        .attr('x', (width/2) - 250)
        .attr('y', 510)
        .attr('width', 500)
        .attr('height', 1)
        .attr('fill', 'none')
        .attr('stroke', 'black')

    //backboard
    g.append('rect')
        .attr('x', (width/2-30))
        .attr('y', 85)
        .attr('width', 60)
        .attr('height', 1)
        .attr('fill', 'none')
        .attr('stroke', 'black')

    //freethrow
    g.append('rect')
        .attr('x',  (width/2 - 80))
        .attr('y', 235)
        .attr('width', 160)
        .attr('height', 1)
        .attr('fill', 'none')
        .attr('stroke', 'black')
    
    // arc around freethrwo line
    g.append("circle")
        .attr("cx", width/2) 
        .attr("cy",235 ) 
        .attr("r", 60) 
        .attr('fill', 'none')
        .attr('stroke', 'black')

    //left side of inner paint
    g.append('rect')
        .attr('x', (width/2) - 60)
        .attr('y', 40)
        .attr('width', 1)
        .attr('height', 195)
        .attr('fill', 'none')
        .attr('stroke', 'black')
    //right side of inner paint
    g.append('rect')
        .attr('x', (width/2) + 60)
        .attr('y', 40)
        .attr('width', 1)
        .attr('height', 195)
        .attr('fill', 'none')
        .attr('stroke', 'black')

    //left side 3
    g.append('rect')
        .attr('x', (width/2)-220)
        .attr('y', 40)
        .attr('width', 1)
        .attr('height', 140)
        .attr('fill', 'none')
        .attr('stroke', 'black')
    //right side 3
    g.append('rect')
        .attr('x', (width/2)+220)
        .attr('y', 40)
        .attr('width', 1)
        .attr('height', 140)
        .attr('fill', 'none')
        .attr('stroke', 'black')

    //g.append("arc")
    //    .innerRadius(0)
    //    .outerRadius(100)
    //    .startAngle(0)
    //    .endAngle(Math.PI / 2)
    //    .attr('x', 600)
    //    .attr('y', 40)

    const arc = d3.arc()
        .innerRadius(237.5) // Adjust as needed
        .outerRadius(237.5) // Adjust as needed
        .startAngle((-Math.PI/2) - (Math.PI / 8.2))
        .endAngle((-3*Math.PI/2) + (Math.PI / 8.2));
      
      g.append("path")
        .attr("d", arc)
        .attr('stroke-width', 2)
        .attr("transform", `translate(${width / 2},92)`)
        .attr("fill", "none")
        .attr("stroke", "black");

    //let dataToShow;

    //$: if (index == 1) {
    //  dataToShow = shotData.filter(shotData.Year === 2003);
    //}
  });

  //const filter_shots0304 = (feature) => {
  //  return (
  //    feature.properties.Year === 2003
  //  );
  //};

  //const shots0304 = shotData.filter(filter_shots0304);
    

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