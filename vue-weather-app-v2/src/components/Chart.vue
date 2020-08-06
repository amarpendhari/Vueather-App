<template>
  <div>
    <div id="chartContainer" style="height: 250px; width: 100%;"></div>
  </div>
</template>

<script src="https://canvasjs.com/assets/script/canvasjs.min.js"></script>
<script>
import moment from "moment-timezone";
import CanvasJS from "../js/canvasjs.min";
export default {
  name: "Chart",
  data() {
    return {};
  },
  methods: {
    Loadchart() {
      var chart = new CanvasJS.Chart("chartContainer", {
        animationEnabled: true,
        data: [
          {
            yValueFormatString: "#,### Units",
            interval: 1,
            intervalType: "hour",
            valueFormatString: "HH:mm",
            type: "spline",
            dataPoints: [
              { x: new Date(2020, 1, 4, 9), y: 25 },
              { x: new Date(2020, 1, 4, 10), y: 27 },
              { x: new Date(2020, 1, 4, 11), y: 33 },
              { x: new Date(2020, 1, 4, 12), y: 29 },
              { x: new Date(2020, 1, 4, 13, 0), y: 30 },
              { x: new Date(2020, 1, 4, 14, 0), y: 23 }
              // { x: new Date(2020, 1, 4, 15, 0), y: 18 }
              // { x: new Date(2020, 1, 4, 16, 0), y: 25 },
              // { x: new Date(2020, 1, 4, 17, 0), y: 27 },
              // { x: new Date(2020, 1, 4, 18, 0), y: 33 },
              // { x: new Date(2020, 1, 4, 19, 0), y: 29 },
              // { x: new Date(2020, 1, 4, 20, 0), y: 30 },
              // { x: new Date(2020, 1, 4, 21, 0), y: 23 },
              // { x: new Date(2020, 1, 4, 22, 0), y: 18 }
            ]
          }
        ]
      });
      chart.render();
    }
  },
  mounted() {
    this.Loadchart();
  }
};
</script>

<style>
.highcharts-figure,
.highcharts-data-table table {
  min-width: 360px;
  max-width: 800px;
  margin: 1em auto;
}

.highcharts-data-table table {
  font-family: Verdana, sans-serif;
  border-collapse: collapse;
  border: 1px solid #ebebeb;
  margin: 10px auto;
  text-align: center;
  width: 100%;
  max-width: 500px;
}
.highcharts-data-table caption {
  padding: 1em 0;
  font-size: 1.2em;
  color: #555;
}
.highcharts-data-table th {
  font-weight: 600;
  padding: 0.5em;
}
.highcharts-data-table td,
.highcharts-data-table th,
.highcharts-data-table caption {
  padding: 0.5em;
}
.highcharts-data-table thead tr,
.highcharts-data-table tr:nth-child(even) {
  background: #f8f8f8;
}
.highcharts-data-table tr:hover {
  background: #f1f7ff;
}
.canvasjs-chart-credit {
  display: none;
}
</style>
