<template>
  <header>
    <Head />
  </header>

  <Dutch />

  <footer>
    <Foot />
  </footer>
</template>

<script>
import Head from "./components/Head.vue";
import Dutch from "./components/Dutch.vue";
import Foot from "./components/Foot.vue";

export default {
  name: "App",
  components: {
    Head,
    Dutch,
    Foot,
  },
};
</script>
<style lang="scss">
@use "./assets/scss/reset.scss";
@use "./assets/scss/variable" as v;
</style>
