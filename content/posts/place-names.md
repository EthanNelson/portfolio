+++ 
draft = true
date = 2019-04-14T18:05:40-06:00
title = "American Place Names"
slug = "place-names" 
tags = ["d3.js", "cartography", "data analysis"]
categories = []
+++

An interactive map of the location quotient of select place name components by county. This is not an exhaustive list of place names, but it does show some neat patterns.


<meta charset="utf-8">
<title>Place Name Endings</title>
<style>
path {
	stroke: #fff;
}
.counties {
  fill: none;
  stroke: #fff;
}

.states {
  fill: none;
  stroke: #fff;
  stroke-width: 2px;
  stroke-linejoin: round;
}
svg {
}

button {
    background-color: #555555; 
    border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    font-size: 16px;
    display: inline-block;
    clear:both;
    float: left;
} 
button:hover {
    background-color: #ccc; 
    border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    color: #000;	
}
.button_clicked {
    background-color: #ccc; 
    border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
} 

</style>
<svg width="960" height="600"></svg>

<script src="https://d3js.org/d3.v4.min.js"></script>
<script src="https://d3js.org/d3-scale-chromatic.v1.min.js"></script>
<script src="https://d3js.org/topojson.v2.min.js"></script>
<script>

var dataIndex = 1;

var svg = d3.select("svg"),
    width = +svg.attr("width"),
    height = +svg.attr("height");

var cities = d3.map();

var path = d3.geoPath();

var burgs_x = d3.scaleLinear()
    .domain([0, 58])
    .rangeRound([600, 860]);

var burgs_color = d3.scaleLinear()
    .domain(d3.range(0, 58))
    .range(d3.schemeBlues[9]);
var monts_color = d3.scaleLinear()
    .domain(d3.range(0, 113))
    .range(d3.schemeBlues[9]);
var forests_color = d3.scaleLinear()
    .domain(d3.range(0, 200))
    .range(d3.schemeBlues[9]);
var shires_color = d3.scaleLinear()
    .domain(d3.range(0, 500))
    .range(d3.schemeBlues[9]);
var lakes_color = d3.scaleLinear()
    .domain(d3.range(0, 76))
    .range(d3.schemeBlues[9]);
var washingtons_color = d3.scaleLinear()
    .domain(d3.range(0, 550))
    .range(d3.schemeBlues[9]);
var jeffersons_color = d3.scaleLinear()
    .domain(d3.range(0, 550))
    .range(d3.schemeBlues[9]);
var franklins_color = d3.scaleLinear()
    .domain(d3.range(0, 800))
    .range(d3.schemeBlues[9]);
var beaches_color = d3.scaleLinear()
    .domain(d3.range(0, 200))
    .range(d3.schemeBlues[9]);
// d3.queue()
//     .defer(d3.json, "geo/counties.json")
//     //.defer(d3.csv, "data/cities_data.csv", function(d) { cities.set(d.id, +d.burgs_lq); })
//     .await(ready);

d3.json("geo/counties.json", function(error, us) {

  svg.append("g")
      .attr("class", "counties")
    .selectAll("path")
    .data(topojson.feature(us, us.objects.counties).features)
    .enter().append("path")
      .attr("fill", function(d) {
      	if (d.properties.burgs_lq === 0) {
      		return "#ededed";
      	}
      	else {
      		return burgs_color(d.properties.burgs_lq);}
  		})
      .attr("d", path)
    .append("title")
      .text(function(d) { return d.properties.county_name + ": " + d3.format(".2f")(d.properties.burgs_lq); });

  svg.append("path")
      .datum(topojson.mesh(us, us.objects.states, function(a, b) { return a !== b; }))
      .attr("class", "states")
      .attr("d", path);
//burgs
d3.select("body").append("button")
    .text("Burgs")
    .on("click", function () {
	var appending = svg.selectAll("g")
    	.data(topojson.feature(us, us.objects.counties).features)
    	.attr("class","counties");
    	appending.enter().append("path")
      .attr("fill", function(d) {
      	if (d.properties.burgs_lq === 0) {
      		return "#ededed";
      	}
      	else {
      		return beaches_color(d.properties.burgs_lq);}
  		})
      .attr("d", path)
    .append("title")
      .text(function(d) { return d.properties.county_name + ": " + d3.format(".2f")(d.properties.burgs_lq); });

  svg.append("path")
      .datum(topojson.mesh(us, us.objects.states, function(a, b) { return a !== b; }))
      .attr("class", "states")
      .attr("d", path);

	appending.exit().remove();
})      
//forests
d3.select("body").append("button")
    .text("Forests")
    .on("click", function () {
	var appending = svg.selectAll("g")
    	.data(topojson.feature(us, us.objects.counties).features)
    	.attr("class","counties");
    	appending.enter().append("path")
      .attr("fill", function(d) {
      	if (d.properties.forests_lq === 0) {
      		return "#ededed";
      	}
      	else {
      		return burgs_color(d.properties.forests_lq);}
  		})
      .attr("d", path)
    .append("title")
      .text(function(d) { return d.properties.county_name + ": " + d3.format(".2f")(d.properties.forests_lq); });

  svg.append("path")
      .datum(topojson.mesh(us, us.objects.states, function(a, b) { return a !== b; }))
      .attr("class", "states")
      .attr("d", path);

	appending.exit().remove();

})
//monts
d3.select("body").append("button")
    .text("Monts")
    .on("click", function () {
	var appending = svg.selectAll("g")
    	.data(topojson.feature(us, us.objects.counties).features)
    	.attr("class","counties");
    	appending.enter().append("path")
      .attr("fill", function(d) {
      	if (d.properties.monts_lq === 0) {
      		return "#ededed";
      	}
      	else {
      		return burgs_color(d.properties.monts_lq);}
  		})
      .attr("d", path)
    .append("title")
      .text(function(d) { return d.properties.county_name + ": " + d3.format(".2f")(d.properties.monts_lq); });

  svg.append("path")
      .datum(topojson.mesh(us, us.objects.states, function(a, b) { return a !== b; }))
      .attr("class", "states")
      .attr("d", path);

	appending.exit().remove();

})
//shires
d3.select("body").append("button")
    .text("Shires")
    .on("click", function () {
	var appending = svg.selectAll("g")
    	.data(topojson.feature(us, us.objects.counties).features)
    	.attr("class","counties");
    	appending.enter().append("path")
      .attr("fill", function(d) {
      	if (d.properties.shires_lq === 0) {
      		return "#ededed";
      	}
      	else {
      		return burgs_color(d.properties.shires_lq);}
  		})
      .attr("d", path)
    .append("title")
      .text(function(d) { return d.properties.county_name + ": " + d3.format(".2f")(d.properties.shires_lq); });

  svg.append("path")
      .datum(topojson.mesh(us, us.objects.states, function(a, b) { return a !== b; }))
      .attr("class", "states")
      .attr("d", path);

	appending.exit().remove();
})
//beaches
d3.select("body").append("button")
    .text("Beaches")
    .on("click", function () {
	var appending = svg.selectAll("g")
    	.data(topojson.feature(us, us.objects.counties).features)
    	.attr("class","counties");
    	appending.enter().append("path")
      .attr("fill", function(d) {
      	if (d.properties.beaches_lq === 0) {
      		return "#ededed";
      	}
      	else {
      		return beaches_color(d.properties.beaches_lq);}
  		})
      .attr("d", path)
    .append("title")
      .text(function(d) { return d.properties.county_name + ": " + d3.format(".2f")(d.properties.beaches_lq); });

  svg.append("path")
      .datum(topojson.mesh(us, us.objects.states, function(a, b) { return a !== b; }))
      .attr("class", "states")
      .attr("d", path);

	appending.exit().remove();
})    
//lakes
d3.select("body").append("button")
    .text("Lakes")
    .on("click", function () {
	var appending = svg.selectAll("g")
    	.data(topojson.feature(us, us.objects.counties).features)
    	.attr("class","counties");
    	appending.enter().append("path")
      .attr("fill", function(d) {
      	if (d.properties.lakes_lq === 0) {
      		return "#ededed";
      	}
      	else {
      		return burgs_color(d.properties.lakes_lq);}
  		})
      .attr("d", path)
    .append("title")
      .text(function(d) { return d.properties.county_name + ": " + d3.format(".2f")(d.properties.lakes_lq); });

  svg.append("path")
      .datum(topojson.mesh(us, us.objects.states, function(a, b) { return a !== b; }))
      .attr("class", "states")
      .attr("d", path);

	appending.exit().remove();
})
//Washingtons
d3.select("body").append("button")
    .text("Washingtons")
    .on("click", function () {
	var appending = svg.selectAll("g")
    	.data(topojson.feature(us, us.objects.counties).features)
    	.attr("class","counties");
    	appending.enter().append("path")
      .attr("fill", function(d) {
      	if (d.properties.washingtons_lq === 0) {
      		return "#ededed";
      	}
      	else {
      		return burgs_color(d.properties.washingtons_lq);}
  		})
      .attr("d", path)
    .append("title")
      .text(function(d) { return d.properties.county_name + ": " + d3.format(".2f")(d.properties.washingtons_lq); });

  svg.append("path")
      .datum(topojson.mesh(us, us.objects.states, function(a, b) { return a !== b; }))
      .attr("class", "states")
      .attr("d", path);

	appending.exit().remove();
})
//jeffersons
d3.select("body").append("button")
    .text("Jeffersons")
    .on("click", function () {
	var appending = svg.selectAll("g")
    	.data(topojson.feature(us, us.objects.counties).features)
    	.attr("class","counties");
    	appending.enter().append("path")
      .attr("fill", function(d) {
      	if (d.properties.jeffersons_lq === 0) {
      		return "#ededed";
      	}
      	else {
      		return burgs_color(d.properties.jeffersons_lq);}
  		})
      .attr("d", path)
    .append("title")
      .text(function(d) { return d.properties.county_name + ": " + d3.format(".2f")(d.properties.jeffersons_lq); });

  svg.append("path")
      .datum(topojson.mesh(us, us.objects.states, function(a, b) { return a !== b; }))
      .attr("class", "states")
      .attr("d", path);

	appending.exit().remove();
})
//franklins
d3.select("body").append("button")
    .text("Franklins")
    .on("click", function () {
	var appending = svg.selectAll("g")
    	.data(topojson.feature(us, us.objects.counties).features)
    	.attr("class","counties");
    	appending.enter().append("path")
      .attr("fill", function(d) {
      	if (d.properties.franklins_lq === 0) {
      		return "#ededed";
      	}
      	else {
      		return burgs_color(d.properties.franklins_lq);}
  		})
      .attr("d", path)
    .append("title")
      .text(function(d) { return d.properties.county_name + ": " + d3.format(".2f")(d.properties.franklins_lq); });

  svg.append("path")
      .datum(topojson.mesh(us, us.objects.states, function(a, b) { return a !== b; }))
      .attr("class", "states")
      .attr("d", path);

	appending.exit().remove();
})

})
</script>