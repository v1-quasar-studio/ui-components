<template>
  <q-page class="flex flex-center">
   <local-new-component></local-new-component>
  </q-page>
</template>

<script>
import newComponent from "../components/new-component/index.vue";
export default {
  components: {
    "local-new-component": newComponent
  },
  data() {
    return {
    };
  }
};
</script>
