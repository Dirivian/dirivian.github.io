---
layout: default
permalink: /pages/interactive/eda/
---



<meta charset="utf-8">
<style>
  .state-borders {
    fill: none;
    stroke: #fff;
    stroke-width: 0.5px;
    stroke-linejoin: round;
    stroke-linecap: round;
    pointer-events: none;
  }
</style>

<body>

  <script src="//d3js.org/d3.v5.min.js"></script>
  <script src="//d3js.org/d3.v4.min.js"></script>
  <script src="https://d3js.org/topojson.v3.min.js"></script>
  <script src="https://d3js.org/d3-array.v1.min.js"></script>
<script src="https://d3js.org/d3-geo.v1.min.js"></script>
<script src="https://d3js.org/d3-geo-projection.v2.min.js"></script>
  <script>
    var width = 1500,
      height = 2000;

    
    var path = d3.geoPath().projection(d3.geoMiller());

    var svg = d3.select("body").append("svg")
      .attr("width", width)
      .attr("height", height);
    var valueById={};
    var projection = d3.geoMiller();

var projected_transform = function(x,y)
{return "translate(" + projection([x,y]) + ")";}
var elephant 
d3.csv("earthquakes.csv",function(earthquakes){
  earthquakes.forEach(function(d){
    d["impact.significance"] = +d["impact.significance"]
    d["location.longitude"] = +d["location.longitude"] 
    d["location.latitude"] = +d["location.latitude"] 
  });
  elephant = earthquakes





    d3.json("geo.json", function(error, geo) {
      svg.selectAll("path")
        .attr("class", "state-borders")
        .data(topojson.feature(geo, geo.objects.countries).features)
        .enter().append("path")
        .style("opacity", 0.3)
        .attr("d", path);
      })
    svg.selectAll("circle")
        .data(elephant)
        .enter()
        .append("circle")
          .attr("transform", function(d) {return projected_transform(d["location.longitude"],d["location.latitude"])})

          .attr("r", function(d) {return 0.01*d["impact.significance"]})
          .style("fill","red")
          .style("opacity", 0.95)


}); 


  </script>


