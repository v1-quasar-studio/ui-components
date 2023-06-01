<template>
  <q-page class="flex flex-center">
    <!-- <local-new-component></local-new-component> -->
    <local-zing-component
      :chartType="'area'"
      :height="'270px'"
      :hideLegend="true"
      :hideZeros="false"
      :labels="labels"
      :scaleXTooltip="true"
      :scaleYShortValues="true"
      :scrollX="true"
      :series="series"
      :smallScaleYValues="false"
      :stacked="false"
      :twoYAxis="true"
      :xLabel="''"
      :yLabel="''"
      :zoomSize="6"
    ></local-zing-component>
  </q-page>
</template>

<script>
// import newComponent from "../components/new-component/index.vue";
import zingComponent from "../components/zing-component/index.vue";
import { labels, series } from "./data.js";
export default {
  components: {
    // "local-new-component": newComponent
    "local-zing-component": zingComponent
  },
  data() {
    return {
      labels,
      series
    };
  }
};
</script>
