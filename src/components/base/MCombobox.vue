<template>
  <div
    class="m-combobox"
    :class="hasIcon === 'false' ? 'm-combobox-mini' : ''"
    @click="openCombobox"
    @keyup.enter="openCombobox"
    :code="this.code"
  >
    <div class="icon">
      <div class="icon-filter"></div>
    </div>

    <input
      class="input"
      type="text"
      :code="this.code"
      :value="this.name"
      readonly
    />

    <div class="up-down">
      <div class="down"><div class="btn icon-down__black"></div></div>
    </div>

    <div class="drop-down" v-if="isShow">
      <div
        class="drop-down__item"
        :class="item.code == code ? 'active' : ''"
        @click="
          this.code = item.code;
          this.name = item.name;
        "
        v-for="item in items"
        :key="item"
      >
        {{ item.name }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    hasIcon: {
      type: String,
      default: "true",
    },
    items: {
      type: Array,
      default() {
        return [{}];
      },
    },
    title: {
      type: String,
    },
  },
  data() {
    return {
      isShow: false,
      name: "",
      code: "",
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
  mounted() {
    /**
     * khởi tạo giá trị ban đầu cho combobox
     * Author: TTDuc (07/08/2022)
     */
    if (this.title) {
      this.name = this.title;
    } else {
      if (this.items.length > 0) {
        this.name = this.items[0].name;
        this.code = this.items[0].code;
      }
    }
  },
};
</script>

<style scoped>
@import url(../../css/base/combobox.css);
</style>
