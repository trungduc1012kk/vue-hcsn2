<template>
  <div class="menu">
    <div class="menu-top">
      <div class="brand">
        <div class="icon-logo logo"></div>
        <h1 class="brand__text" v-if="isZoomOut">MISA QLTS</h1>
      </div>
      <ul class="navbar">
        <li class="nav-item">
          <div class="icon">
            <div class="icon-tivi"></div>
          </div>
          <div class="nav-item__text" v-if="isZoomOut">Tổng quan</div>
        </li>
        <li class="nav-item active">
          <div class="icon">
            <div class="icon-oto"></div>
          </div>
          <div class="nav-item__text" v-if="isZoomOut">Tài sản</div>
        </li>
        <li class="nav-item">
          <div class="icon"><div class="icon-street"></div></div>
          <div class="nav-item__text" v-if="isZoomOut">Tài sản HT-DB</div>
        </li>
        <li class="nav-item">
          <div class="icon"><div class="icon-tool"></div></div>
          <div class="nav-item__text" v-if="isZoomOut">Công cụ công dụng</div>
        </li>
        <li class="nav-item">
          <div class="icon"><div class="icon-category"></div></div>
          <div class="nav-item__text" v-if="isZoomOut">Danh mục</div>
        </li>
        <li class="nav-item">
          <div class="icon"><div class="icon-search"></div></div>
          <div class="nav-item__text" v-if="isZoomOut">Tra cứu</div>
        </li>
        <li class="nav-item">
          <div class="icon"><div class="icon-report"></div></div>
          <div class="nav-item__text" v-if="isZoomOut">Báo cáo</div>
        </li>
      </ul>
    </div>
    <div class="menu-bottom">
      <button class="btn zoom-in" id="zoom" @click="zoomNavbar">
        <div class="btn__icon center">
          <div :class="isZoomOut ? 'icon-left' : 'icon-right'"></div>
        </div>
      </button>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      isZoomOut: true,
    };
  },
  methods: {
    /**
     * hàm bắt sự kiện thu phóng navbar
     * Author: TTDuc(07/08/2022)
     */
    zoomNavbar() {
      this.isZoomOut = !this.isZoomOut;
      this.$emit("zoomNavbar");
    },
  },
};
</script>
