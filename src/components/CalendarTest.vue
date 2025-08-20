<template>
  <div class="map-container">
    <div ref="calRef" id="ex-wind"></div>
    <!-- <a
      className="button button--sm button--secondary margin-top--sm"
      href="#"
      @click="handlePrev"
    >
      ← Previous
    </a>
    <a
      className="button button--sm button--secondary margin-left--xs margin-top--sm"
      href="#"
      @click="handleNext"
    >
      Next →
    </a> -->
    <div id="ex-wind-legend" style="float: right"></div>
  </div>
</template>

<script>
import * as d3 from "d3";
window.d3 = d3;
import CalHeatMap from "cal-heatmap";
import "cal-heatmap/cal-heatmap.css";
import Tooltip from "cal-heatmap/plugins/Tooltip";
import Legend from "cal-heatmap/plugins/Legend";

export default {
  data() {
    return {
      cal: null,
      domain: "month",
      subDomain: "day",
    };
  },
  mounted() {
    this.initHeatMap();
  },
  methods: {
    handlePrev(e) {
      e.preventDefault();
      this.cal.previous();
    },
    handleNext(e) {
      e.preventDefault();
      this.cal.next();
    },
    async initHeatMap() {
      this.cal = new CalHeatMap();
      this.cal.paint(
        {
          data: {
            source: "/weather.csv",
            type: "csv",
            x: "date",
            y: (d) => +d["wind"],
            groupY: "max",
          },
          date: { start: new Date("2012-01-01") },
          range: 12,
          scale: {
            color: {
              type: "quantize",
              scheme: "burd",
              domain: [0, 1, 2, 3, 4, 5, 6, 7],
            },
          },
          domain: {
            type: this.domain,
            dynamicDimension: false,
          },
          subDomain: { type: this.subDomain, radius: 2 },
          itemSelector: "#ex-wind",
        },
        [
          [
            Tooltip,
            {
              text: function (date, value, dayjsDate) {
                return (
                  (value ? value + "km/h" : "No data") +
                  " on " +
                  dayjsDate.format("LL")
                );
              },
            },
          ],
          [
            Legend,
            {
              tickSize: 0,
              width: 100,
              itemSelector: "#ex-wind-legend",
              label: "Seattle wind (km/h)",
            },
          ],
        ]
      );
    },
  },
};
</script>

<style scoped>
.map-container {
  height: fit-content;
  width: fit-content;
  padding: 20px;
  position: relative;
  color: #2c3e50;
}
</style>
