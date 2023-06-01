<template>
  <div>
    <line-area-bar-chart
      :chartType="chartType.value"
      :height="height"
      :labels="labels"
      :series="chartSeries"
      :xLabel="xLabel"
      :yLabel="yLabel"
      :showRanges="showRanges"
      :twoYAxis="twoYAxis"
      :scale-x-tooltip="scaleXTooltip"
      :scale-y-short-values="scaleYShortValues"
      :stacked="stacked"
      :hide-zeros="hideZeros"
      :scroll-x="scrollX"
      :zoom-size="zoomSize"
      :hide-legend="hideLegend"
      :small-scale-y-values="smallScaleYValues"
      :plot-style="plotStyle"
      :custom-configuration="customConfiguration"
      :minValue="minValue"
    />
  </div>
</template>

<script>
import {
  LineAreaBarChart,
  LineAreaBarChartColors as colors
} from "zingchart-vue-implementation";

export default {
  components: {
    LineAreaBarChart
  },
  props: {
    height: { type: String, default: "300px" },
    labels: {},
    series: {},
    xLabel: { type: String, default: "" },
    yLabel: { type: String, default: "" },
    showRanges: { type: Boolean, default: false },
    twoYAxis: { type: Boolean },
    scaleXTooltip: Boolean,
    scaleYShortValues: { type: Boolean, default: true },
    stacked: Boolean,
    hideZeros: Boolean,
    scrollX: Boolean,
    zoomSize: Number,
    hideLegend: Boolean,
    smallScaleYValues: Boolean,
    plotStyle: Object,
    customConfiguration: { type: Object, default: () => ({}) },
    minValue: {
      type: Number
    }
  },
  data() {
    return {
      chartType: { value: "line" },
      twoXAxis:0
    };
  },
  computed: {
    chartSeries() {
      return this.series.filter((s, i) => !this.hiddenItems.includes(i));
    }
  }
};
</script>

<style></style>
