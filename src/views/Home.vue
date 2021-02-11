<template>
  <main class="main">
    <div class="preview" v-for="(view, ind) in views" :key="ind">
      <router-link :to="view.router"
        ><img src="../assets/preview/test.jpg" alt="test"
      /></router-link>
    </div>
  </main>
</template>

<script>
// import svgMorphing from "@/components/svg_morphing";
export default {
  name: "Home",
  data() {
    return {
      views: [
        { preview: "/test", title: "", action: "", router: "/svg_morphing" },
        { preview: "", title: "", action: "", router: "" },
        { preview: "", title: "", action: "", router: "" },
      ],
    };
  },
  components: {
    // svgMorfing,
  },
};
</script>

<style>
.main {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  padding: 20px 0 0 20px;
}
.preview {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 300px;
  height: 300px;
  margin-right: 20px;
  margin-bottom: 20px;
  overflow: hidden;
  border: 1px solid #bfccd6;
  box-shadow: 0 2px 12px -2px rgb(0 0 0 / 15%);
  transition: all 0.25s linear;
}
img {
  width: 100%;
  height: auto;
  display: block;
}
</style>
