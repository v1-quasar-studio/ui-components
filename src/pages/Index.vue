<template>
  <q-page class="flex flex-center">
    <cq-date v-model="range" v-slot="{ on }">
      <q-btn @click="on.open()"> {{ range }} </q-btn>
    </cq-date>
  </q-page>
</template>

<script>
import cqDate from "../components/cq-date/index.vue";
export default {
  name: "PageIndex",
  components: {
    "cq-date": cqDate
  },
  data() {
    return {
      range: {}
    };
  }
};
</script>
