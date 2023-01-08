<template>
  <div>
    <div class="row">
      <div class="col-12">{{ from }} - {{ to }}</div>
      <div class="col-6">
        <q-date v-model="from" :events="eventsFn"> </q-date>
      </div>
      <div class="col-6">
        <q-date v-model="to" :events="eventsFn"> </q-date>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      from: "2023/01/01",
      to: "2023/01/04"
    };
  },
  methods: {
    eventsFn(date) {
      return date >= this.from && date <= this.to;
    }
  }
};
</script>

<style></style>
