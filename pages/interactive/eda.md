---
layout: default
permalink: /pages/interactive/eda/
---




<html lang="en">
<style>
  .state-borders {
    fill: none;
    stroke: #fff;
    stroke-width: 0.5px;
    stroke-linejoin: round;
    stroke-linecap: round;
    pointer-events: none;
  }

.tooltip {
    position: absolute;
    width: 200px;
    height: 28px;
    pointer-events: none;
    }
</style>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Earthquakes</title>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.12.1/themes/base/jquery-ui.css">
  <link rel="stylesheet" href="/resources/demos/style.css">
  <script src="https://code.jquery.com/jquery-1.12.4.js"></script>
  <script src="https://code.jquery.com/ui/1.12.1/jquery-ui.js"></script>
   <script src="//d3js.org/d3.v4.min.js"></script>
  <script src="https://d3js.org/topojson.v3.min.js"></script>
  <script src="https://d3js.org/d3-array.v1.min.js"></script>
<script src="https://d3js.org/d3-geo.v1.min.js"></script>
<script src="https://d3js.org/d3-geo-projection.v2.min.js"></script>
  <script>


$(function() {
$( "#assists" ).slider({
range: true,
min: 0,
max: 2700,
values: [ 0, 2700 ],
slide: function( event, ui ) {
$( "#assistamount" ).val( ui.values[ 0 ] + " - " + ui.values[ 1 ] );
sigvalues = ui.values
filterData("impact.significance", sigvalues, timevalues); } });
$( "#assistamount" ).val( $( "#assists" ).slider( "values", 0 ) +
" - " + $( "#assists" ).slider( "values", 1 ) );
});

 </script> 

   <script>
var timevalues = [ 0, 31 ]
var sigvalues = [ 0, 2700 ]

$(function() {
$( "#time" ).slider({
range: true,
min: 0,
max: 31,
values: [ 0, 31 ],
slide: function( event, ui ) {
$( "#timeamount" ).val( ui.values[ 0 ] + " - " + ui.values[ 1 ] );
timevalues = ui.values
filterData("time.epoch", sigvalues, timevalues); } });
$( "#timeamount" ).val( $( "#assists" ).slider( "values", 0 ) +
" - " + $( "#assists" ).slider( "values", 1 ) );
});
 </script> 

</head>
<body>

<b> About Earthquakes</b>


<p>This is an interactive extension to the exploratory data anaysis done on the earthquakes dataset from CORGIS.
  You can see the exploratory data analysis 
<a href="https://dirivian.github.io/pages/eda/">here</a>.

In this interactive visualization, you can select the significance range of the earthquakes you want to study and 
also select the time period in which they appear. The circles represent the significance of the earthquakes. Hovering 
over them highlights them in blue and displays their epicenter.
</p>



<p> <b>Impact(Significance) </b></p>
<div id="assists" class="slider-range"></div>
<label for="assistamount">Significance range:</label>
<input type="text" id="assistamount" readonly style="border:0;
color:#f6931f; font-weight:bold;">


<p> <b>Time(Days) </b></p>
<div id="time" class="slider-range"></div>
<label for="timeamount">Time range:</label>
<input type="text" id="timeamount" readonly style="border:0;
color:#f6931f; font-weight:bold;">

 
 <script> 
    var width = 1500,
      height = 2000;
var tooltip = d3.select("body").append("div")
.attr("class", "tooltip")
.style("opacity", 0);
    
    var path = d3.geoPath().projection(d3.geoMiller());

    var svg = d3.select("body").append("svg")
      .attr("width", width)
      .attr("height", height);
    var valueById={};
    var projection = d3.geoMiller();




var projected_transform = function(x,y)
{return "translate(" + projection([x,y]) + ")";}
var elephant 
d3.json("https://dirivian.github.io/pages/interactive/geo.json", function(error, geo) {
      svg.selectAll("path")
        .attr("class", "state-borders")
        .data(topojson.feature(geo, geo.objects.countries).features)
        .enter().append("path")
        .style("opacity", 0.3)
        .attr("d", path);
      })
svg.append("input")
        .attr("type", "range")
        .attr("min", 0)
        .attr("max", 5)
        .attr("step", "1")
        .attr("id", "year")
        .on("input", function input() {
          update();
        });

var filterData = function(attr, sigrange, timerange){

  var epoch_start = 1469593183550
var epoch_end = 1472183881830
var day_ratio = 30/(epoch_end -epoch_start)
svg.selectAll("circle").remove();
elephant = []
d3.csv("https://dirivian.github.io/pages/interactive/earthquakes.csv",function(earthquakes){
  earthquakes.forEach(function(d){
    d["impact.significance"] = +d["impact.significance"]
    d["location.longitude"] = +d["location.longitude"] 
    d["location.latitude"] = +d["location.latitude"] 
  });
  elephant = []
  elephant = earthquakes.filter(function(d,i){
  
    if (d["impact.significance"] >sigrange[0] ){
if (d["impact.significance"] <sigrange[1] ){
  if (day_ratio*(d["time.epoch"]-epoch_start) >timerange[0] ){
    if (day_ratio*(d["time.epoch"]-epoch_start) <timerange[1] ){
      return true
    }
    return false
    }
    return false
    }
    return false
  }
  return false
  }
  )



    
    svg.selectAll("circle")
        .data(elephant)
        .enter()
        .append("circle")
          .attr("transform", function(d) {return projected_transform(d["location.longitude"],d["location.latitude"])})
          .attr("r", function(d) {return 0.01*(1+d["impact.significance"])})
          .style("opacity","0.5")
          .attr('fill', 'red')
          .on('mouseover', function (d) {
          d3.select(this)
               .attr('fill','blue')
          tooltip.transition()
              .duration(200)
              .style("opacity", .9);
              tooltip.html(d["location.full"])
              .style("left", (d3.event.pageX + 5) + "px")
              .style("top", (d3.event.pageY - 28) + "px");


               })

          .on('mouseout', function (d, i) {
          d3.select(this).transition()
               .duration('50').attr('fill', 'red')
          tooltip.transition()
.duration(500)
.style("opacity", 0);

             })


}); }

 filterData(["impact.significance"], sigvalues, timevalues)

  </script> 

  <div id="slider"></div>
</body>
</html>
