<template>
  <div class="container" :class="isZoom ? 'zoom-in' : ''">
    <the-header />
    <the-menu @zoomNavbar="isZoom = !isZoom" />
    <the-main />
  </div>
</template>

<script>
import TheHeader from "./components/TheHeader.vue";
import TheMain from "./components/TheMain.vue";
import TheMenu from "./components/TheMenu.vue";
export default {
  name: "App",
  components: {
    TheHeader,
    TheMain,
    TheMenu,
  },
  data() {
    return {
      isZoom: false,
    };
  },
};
</script>

<style scoped>
@import url(./css/main.css);
@import url(./css/page/assetsPage.css);
</style>
