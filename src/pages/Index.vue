<template>
  <q-page class="flex flex-center">
   <!-- <local-new-component></local-new-component> -->
   <local-zing-component></local-zing-component>
  </q-page>
</template>

<script>
// import newComponent from "../components/new-component/index.vue";
import zingComponent from "../components/zing-component/index.vue";
export default {
  components: {
    // "local-new-component": newComponent
    "local-zing-component": zingComponent
  },
  data() {
    return {
    };
  }
};
</script>
