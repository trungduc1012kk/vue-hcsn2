<template>
  <div class="paging">
    <div class="paging__item paging__prev" @click="prevPage">
      <div class="icon">
        <div class="icon-prev"></div>
      </div>
    </div>

    <div
      class="paging__item"
      v-for="(Page, index) in arrShow"
      :key="index"
      :class="Page == this.currentPage ? 'active' : ''"
      @click="changeCurrentPage(Page)"
    >
      {{ Page }}
    </div>

    <div class="paging__item paging__next" @click="nextPage">
      <div class="icon">
        <div class="icon-next"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    nextPage() {
      this.$emit("nextPage");
    },
    prevPage() {
      this.$emit("prevPage");
    },
    changeCurrentPage(Page) {
      if (Page != "...") {
        this.selectedPage = Page;
        this.$emit("changeCurrentPage", this.selectedPage);
      }
    },
  },
  data() {
    return {
      numberPageDisplay: 3,
      selectedPage: 0,
    };
  },
  props: {
    currentPage: {
      type: Number,
      required: true,
    },
    maxPage: {
      type: Number,
      required: true,
    },
  },
  computed: {
    arrShow() {
      if (this.maxPage < this.numberPageDisplay) {
        //nếu maxPage < 3 thì hiện 3 trang
        let arr = [];
        for (let i = 1; i <= this.maxPage; i++) {
          arr.push(i);
        }
        return arr;
      }
      if (this.currentPage < this.numberPageDisplay) {
        //hiển thị 2 trang đầu và trang cuối
        return [1, 2, "...", this.maxPage];
      } else if (
        //hiển thị trang đầu trang cuối và trang hiện tại
        this.currentPage >= this.numberPageDisplay &&
        this.currentPage <= this.maxPage - this.numberPageDisplay + 1
      ) {
        return [1, "...", this.currentPage, "...", this.maxPage];
      } else if (this.currentPage >= this.maxPage - this.numberPageDisplay) {
        //hiển thị 2 trang cuối và trang đầu
        return [1, "...", this.maxPage - 1, this.maxPage];
      }
      return [];
    },
  },
};
</script>

<style scoped>
@import url(../../css/main.css);
</style>
