<template>
  <Header />
  <main class="main">
    <router-view />
  </main>
  <Footer />
</template>

<script>
import Header from "../components/Header.vue";
import Footer from "../components/Footer.vue";
export default {
  name: "main-layout",
  components: { Header, Footer },
};
</script>

<style scoped>
</style>
