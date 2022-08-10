<template>
  <div
    class="m-combobox m-combobox-2"
    @click="openCombobox"
    @keyup.enter="openCombobox"
    :name="this.name"
    :code="this.code"
  >
    <input
      class="input"
      type="text"
      :value="this.code"
      :placeholder="this.placeholder"
      readonly
    />

    <div class="up-down">
      <div class="down"><div class="btn icon-down__black"></div></div>
    </div>

    <div class="drop-down" v-if="isShow">
      <div class="drop-down__header">
        <div class="drop-down__item">
          <div class="drop-down__code">Mã</div>
          <div class="drop-down__name">Tên</div>
        </div>
      </div>

      <div class="drop-down__body">
        <div
          class="drop-down__item"
          :class="item.code == code ? 'active' : ''"
          @click="this.code = item.code"
          v-for="item in items"
          :key="item"
        >
          <div class="drop-down__code">{{ item.code }}</div>
          <div class="drop-down__name">{{ item.name }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isShow: false,
      placeholder: "Nhập giá trị ",
      name: "",
      code: "",
      items: [
        { id: 1, code: "CN", name: "cá nhân" },
        { id: 2, code: "TT", name: "tập thể" },
        { id: 3, code: "K", name: "khác" },
        { id: 4, code: "OK", name: "cá nhân" },
        { id: 5, code: "CD", name: "tập thể" },
        { id: 6, code: "NPM", name: "khác" },
      ],
    };
  },
  methods: {
    /**
     * khởi tạo hàm mở combobox
     * Author: TTDuc (06/08/2022)
     */
    openCombobox() {
      this.isShow = !this.isShow;
    },
  },
};
</script>

<style scoped>
@import url(../../css/base/combobox.css);
</style>
