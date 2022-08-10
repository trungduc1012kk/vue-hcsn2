<template>
  <div id="context-menu" @click="close">
    <div
      class="context-menu__content"
      :style="{ top: posTop + 'px', left: posLeft + 'px' }"
    >
      <div class="context-menu__item">
        <div class="icon">
          <div class="icon-add"></div>
        </div>
        <div class="text">Thêm tài sản</div>
      </div>
      <div class="context-menu__item">
        <div class="icon">
          <div class="icon-edit"></div>
        </div>
        <div class="text">Sửa tài sản</div>
      </div>
      <div class="context-menu__item">
        <div class="icon">
          <div class="icon-delete__black"></div>
        </div>
        <div class="text">Xóa tài sản</div>
      </div>
      <div class="context-menu__item">
        <div class="icon">
          <div class="icon-copy"></div>
        </div>
        <div class="text">Nhân bản tài sản</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    posTop: {
      type: Number,
      default: 100000,
    },
    posLeft: {
      type: Number,
      default: 100000,
    },
  },
  methods: {
    close() {
      this.$emit("close");
    },
  },
};
</script>

<style scoped>
@import url(./../../css/layout/contextMenu.css);
</style>
