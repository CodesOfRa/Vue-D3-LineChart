<template>
  <svg id="myLineChart" ref="myLineChart" width="600px" height="600px"></svg>
</template>
<script>
import * as d3 from "d3";
export default {
  props: ["data"],
  mounted() {
    this.drawChart();
  },
  methods: {
    drawChart() {
      var margin = { top: 10, right: 20, bottom: 30, left: 30 },
        width = 600 - margin.left - margin.right,
        height = 600 - margin.top - margin.bottom;

      var n = this.data.length;
      var xScale = d3
        .scaleLinear()
        .domain([0, n - 1]) // input
        .range([0, width]); // output

      var yScale = d3
        .scaleLinear()
        .domain([105, 123]) // input
        .range([height, 0]); // output

      var line = d3
        .line()
        .x(function(d, i) {
          return xScale(i);
        })
        .y(function(d) {
          return yScale(d.y);
        });
      var dataset = this.data;

      var svg = d3
        .select("#myLineChart")
        .append("svg")
        .attr("width", width + margin.left + margin.right)
        .attr("height", height + margin.top + margin.bottom)
        .append("g")
        .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

      svg
        .append("g")
        .attr("class", "x axis")
        .attr("transform", "translate(0," + height + ")")
        .call(d3.axisBottom(xScale).ticks(7));

      svg
        .append("g")
        .attr("class", "y axis")
        .call(d3.axisLeft(yScale).ticks(5));
      svg
        .append("path")
        .datum(dataset)
        .attr("class", "line")
        .attr("d", line)
        .call(function(path) {
          path
            .transition()
            .duration(2500)
            .attrTween("stroke-dasharray", function() {
              var l = this.getTotalLength(),
                i = d3.interpolateString("0," + l, l + "," + l);
              return function(t) {
                return i(t);
              };
            });
        });

      svg
        .selectAll(".dot")
        .data(dataset)
        .enter()
        .append("circle")
        .attr("class", "dot")
        .attr("cx", function(d, i) {
          return xScale(i);
        })
        .attr("cy", function(d) {
          return yScale(d.y);
        })
        .attr("r", 3);
    }
  }
};
</script>
<style>
.line {
  fill: none;
  stroke: #11a3d8;
  stroke-width: 1.2;
}
.dot {
  fill: #989a99;
  stroke: #fff;
}
.tick > line.currentColor {
  stroke: #989a99;
}
.x.axis > .tick > line {
  stroke: white;
}
.x.axis > .domain,
.y.axis > .domain {
  stroke: #989a99;
}
.y.axis > .tick > line {
  stroke: #989a99;
}
.y.axis > .tick > text,
.x.axis > .tick > text {
  color: #989a99;
}
</style>

