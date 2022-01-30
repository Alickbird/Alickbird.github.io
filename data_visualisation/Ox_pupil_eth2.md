---
layout: default
---
[back](./)

<h3>Oxfordshire Schools Pupil Ethnicity 2021</h3>

<!-- Load d3.js -->
<script src="https://d3js.org/d3.v4.js"></script>

<script>
function val() {
    d = document.getElementById("EL").value;
    return(d)
}
</script>

<!--Add E/L filter-->
<select id="EL" onchange="update(val())">
  <option value="Count" >% Ethnic Minority</option>
  <option value="Lcount" >% Non English First Language</option>
</select>

<!--Add sector filter-->
<select id="Sector" onchange="update(val())">
  <option value="Total">Total</option>
  <option value="Primary">Primary</option>
  <option value="Secondary">Secondary</option>
</select>

<!-- Create a div where the graph will take place -->
<div id="my_dataviz"></div>

<script>

// set the dimensions and margins of the graph
var margin = {top: 30, right: 30, bottom: 70, left: 135};
var  width = 370;
var  height = 300;

// append the svg object to the body of the page
var svg = d3.select("#my_dataviz")
  .append("svg")
    .attr("width", width + margin.left + margin.right)
    .attr("height", height + margin.top + margin.bottom)
  .append("g")
    .attr("transform",
          "translate(" + margin.left + "," + margin.top + ")");

// Initialize the Y axis
var y = d3.scaleBand()
  .range([ 0, height])
  .padding(0.2);
var yAxis = svg.append("g")
  .attr("fill","black")


// Initialize the X axis
var x = d3.scaleLinear()
  .range([0, width]);

// hide x axis
//var yAxis = svg.append("g")
//  .attr("class","myYaxis")

// A function that create / update the plot for a given variable:
function update(selectedVar) {

  // Parse the Data
  d3.csv("https://raw.githubusercontent.com/Alickbird/OxInsight-charts/main/Ethnicity_article_data.csv", function(data) {

    // filter data
    var selection = d3.select("#Sector").node().value
    data = data.filter(function(d){return d.PorS == selection}); 

    // Y axis
    y.domain(data.map(function(d) { return d.District ; }))
    yAxis.transition().duration(1000).call(d3.axisLeft(y)).selectAll("text").attr("font-size" , "13px")
    console.log(yAxis)

    // Add X axis - swapped
    x.domain([0, 0.6]);

    // hide x axis
    //   xAxis.transition().duration(1000).call(d3.axisBottom(y).tickFormat(d3.format(".0%")));

    // variable u: map data to existing bars
    var u = svg.selectAll("rect")
      .data(data)
    // update bars
    u
      .enter()
      .append("rect")
      .merge(u)
      .transition()
      .duration(1000)
        .attr("y", function(d) { return y(d.District ); })
        .attr("x", x(0) ) 
        .attr("height", y.bandwidth())
        .attr("width", function(d) { return x(d[selectedVar]); })
        .attr("fill", function(d) { if (d.District == "Oxfordshire") { return "#00483A";} else {return "#667088";} })

    //formatter for labels
    var formatter = d3.format(".0%");

    // update labels
    var z = svg.selectAll(".barText")
      .data(data)
    z
      .enter()
      .append("text")
      .merge(z)
      .transition()
      .duration(1000)
         .attr("class", "barText")
         .attr("y", function(d, i) {return y(d.District)+20;})
         .attr("x", x(0)+3) 
         .text( function(d) {return formatter(d[selectedVar]);})
         .attr("fill", "white")
         .attr("font-family" , "sans-serif")
         .attr("font-size" , "14px")
  })

}

// Initialize plot
update('Count')

</script>


