<template>
  <MainLayout />
</template>

<script>
import MainLayout from "./layout/MainLayout";

export default {
  name: "App",
  components: {
    MainLayout,
  },
};
</script>
<style>
body, html  {
  margin: 0;
  height: 100%;
}
#app {
  height: 100vh;
}
</style>
