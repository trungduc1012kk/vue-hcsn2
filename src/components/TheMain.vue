<template>
  <div class="main">
    <div class="main-controler">
      <div class="main-controler__left">
        <div class="form-input">
          <div class="icon">
            <div class="icon-search__black"></div>
          </div>
          <input class="input input-icon" type="text" placeholder="Tìm kiếm tài sản" />
        </div>
        <m-combobox :items="arrPropertyType" title="Loại tài sản" />
        <m-combobox :items="arrDepartmentName" title="Bộ phận sử dụng" />
      </div>
      <div class="main-controler__right">
        <button @click="addProperty" class="button">+Thêm tài sản</button>
        <button class="btn">
          <div class="icon">
            <div class="icon-excel"></div>
          </div>
        </button>
        <button class="btn">
          <div class="icon">
            <div class="icon-delete"></div>
          </div>
        </button>
      </div>
    </div>

    <div id="table">
      <div class="table">
        <table>
          <thead>
            <tr>
              <th class="text-center width-fit">
                <input type="checkbox" @click="selectedAllItem" :checked="selectedProperties == properties" />
              </th>
              <th class="text-center">STT</th>
              <th>Mã tài sản</th>
              <th>Loại tài sản</th>
              <th>Bộ phận sử dụng</th>
              <th class="text-right">Số lượng</th>
              <th class="text-right">Nguyên giá</th>
              <th class="text-right">HM/KH lũy kế</th>
              <th class="text-right">Giá trị còn lại</th>
              <th class="text-center">Chức năng</th>
            </tr>
          </thead>

          <tbody>
            <tr v-for="(property, index) in properties" :key="property" @click="selectedItem(property)"
              :class="selectedProperties.includes(property) ? 'active' : ''" @contextmenu="eventContextMenu">
              <td class="text-center">
                <input type="checkbox" :checked="selectedProperties.includes(property) ? true : false" />
              </td>
              <td class="text-center">{{ index + 1 }}</td>
              <td>{{ property.propertyCode }}</td>
              <td>{{ property.propertyType }}</td>
              <td>{{ property.departmentName }}</td>
              <td class="text-right">{{ property.quantity }}</td>
              <td class="text-right">
                {{ formatMoney(property.MarkedPrice) }}
              </td>
              <td class="text-right">
                {{ formatMoney(property.MarkedPrice - property.attritionValue) }}
              </td>
              <td class="text-right">
                {{ formatMoney(property.attritionValue) }}
              </td>
              <td class="text-center">
                <div class="trow-control">
                  <div class="icon">
                    <div class="icon-edit"></div>
                  </div>
                  <div class="icon">
                    <div class="icon-copy"></div>
                  </div>
                </div>
              </td>
            </tr>
          </tbody>
          <m-context-menu :posTop="posTop" :posLeft="posLeft" v-if="isShowContextMenu" @close="closeContextMenu" />
          <thead>
            <tr>
              <td colspan="5">
                <div class="table-footer">
                  <div class="total-Property">
                    Tổng số: <span>200 bản ghi</span>
                  </div>
                  <m-combobox class="footer-combobox" hasIcon="false" :items="arrPage" />
                  <m-paging :maxPage="maxPage" :currentPage="currentPage" @nextPage="nextPage" @prevPage="prevPage"
                    @changeCurrentPage="changeCurrentPage" />
                </div>
              </td>
              <td class="bold text-right">
                {{ total(properties, "quantity") }}
              </td>
              <td class="bold text-right">
                {{ formatMoney(total(properties, "MarkedPrice")) }}
              </td>
              <td class="bold text-right">
                {{
                    formatMoney(
                      total(properties, "MarkedPrice") - total(properties, "attritionValue")
                    )
                }}
              </td>
              <td class="bold text-right">
                {{ formatMoney(total(properties, "attritionValue")) }}
              </td>
              <td class="bold"></td>
            </tr>
          </thead>
        </table>
      </div>
    </div>
  </div>
  <form-detail :isShow="isShowDetail" @closeForm="toggleFormDetail" :item="currentProperty" />
</template>

<script>
import MCombobox from "./base/MCombobox.vue";
import FormDetail from "./base/MFormDetail.vue";
import MPaging from "./base/MPaging.vue";
import MContextMenu from "./base/MContextMenu.vue";

export default {
  components: {
    MCombobox,
    FormDetail,
    MPaging,
    MContextMenu,
  },
  data() {
    return {
      posTop: 100000,
      posLeft: 100000,
      isShowContextMenu: false,
      totalMarkedPrice: 0,
      totalAttritionValue: 0,
      totalAttritionRate: 0,
      totalQuantity: 0,
      currentPage: 1,
      maxPage: 15,
      selectedProperties: [],
      isShowDetail: false,
      currentProperty: [],
      properties: [
        {
          propertyCode: "TS1231",
          propertyType: "cá nhân",
          departmentName: "Phòng hành chính",
          quantity: 15,
          MarkedPrice: 1000000,
          attritionRate: 1.5,
          attritionValue: 900000,
        },
        {
          propertyCode: "TS1222",
          propertyType: "cá nhân",
          departmentName: "Phòng hành chính",
          quantity: 3,
          MarkedPrice: 123223,
          attritionRate: 1.5,
          attritionValue: 67867,
        },
        {
          propertyCode: "TS4334",
          propertyType: "cá nhân",
          departmentName: "Phòng hành chính",
          quantity: 213,
          MarkedPrice: 12321,
          attritionRate: 3.6,
          attritionValue: 444222,
        },
        {
          propertyCode: "TS1784",
          propertyType: "cá nhân",
          departmentName: "Phòng hành chính",
          quantity: 15,
          MarkedPrice: 1000000,
          attritionRate: 1.5,
          attritionValue: 900000,
        },
        {
          propertyCode: "TS9234",
          propertyType: "cá nhân",
          departmentName: "Phòng hành chính",
          quantity: 15,
          MarkedPrice: 1000000,
          attritionRate: 1.5,
          attritionValue: 900000,
        },
        {
          propertyCode: "TS2234",
          propertyType: "cá nhân",
          departmentName: "Phòng hành chính",
          quantity: 1,
          MarkedPrice: 1232228,
          attritionRate: 1.5,
          attritionValue: 4563432,
        },
        {
          propertyCode: "TS1234",
          propertyType: "Tập thể",
          departmentName: "Phòng hành chính",
          quantity: 15,
          MarkedPrice: 12321213,
          attritionRate: 1.5,
          attritionValue: 3333,
        },
        {
          propertyCode: "TS1234",
          propertyType: "Xe máy",
          departmentName: "Phòng hành chính",
          quantity: 15,
          MarkedPrice: 32323,
          attritionRate: 1.5,
          attritionValue: 900000,
        },
        {
          propertyCode: "TS1234",
          propertyType: "cá nhân",
          departmentName: "Phòng hành chính",
          quantity: 15,
          MarkedPrice: 12,
          attritionRate: 1.5,
          attritionValue: 23,
        },
        {
          propertyCode: "TS1234",
          propertyType: "cá nhân",
          departmentName: "Phòng hành chính",
          quantity: 15,
          MarkedPrice: 1000000,
          attritionRate: 1.5,
          attritionValue: 44,
        },
        {
          propertyCode: "TS1234",
          propertyType: "cá nhân",
          departmentName: "Phòng hành chính",
          quantity: 15,
          MarkedPrice: 56,
          attritionRate: 1.5,
          attritionValue: 34,
        },
        {
          propertyCode: "TS1234",
          propertyType: "cá nhân",
          departmentName: "Phòng hành chính",
          quantity: 44,
          MarkedPrice: 10234000,
          attritionRate: 1.5,
          attritionValue: 24324,
        },
        {
          propertyCode: "TS1234",
          propertyType: "cá nhân",
          departmentName: "Phòng hành chính",
          quantity: 122,
          MarkedPrice: 13234,
          attritionRate: 1.5,
          attritionValue: 897768,
        },
        {
          propertyCode: "TS1234",
          propertyType: "cá nhân",
          departmentName: "Phòng hành chính",
          quantity: 3,
          MarkedPrice: 3454534,
          attritionRate: 1.5,
          attritionValue: 2222,
        },
      ],
      arrPage: [
        { code: 1, name: 15 },
        { code: 2, name: 20 },
        { code: 3, name: 25 },
        { code: 4, name: 30 },
        { code: 5, name: 35 },
      ],
      arrPropertyType: [
        { code: 2, name: "Máy tính xách tay" },
        { code: 3, name: "Bàn ghế" },
        { code: 4, name: "Máy tính bàn" },
      ],
      arrDepartmentName: [
        { code: 2, name: "Bảo vệ" },
        { code: 3, name: "Nhân sự" },
        { code: 4, name: "Hành chính" },
      ],
    };
  },
  methods: {
    /**
     * close contextMenu
     * Author : TTDuc (08/08/2022)
     */
    closeContextMenu() {
      this.toggleContextMenu();
    },
    /**
     * khởi tại sự kiện ẩn hiện contextmenu
     * Author: TTDuc (08/08/2022)
     */
    toggleContextMenu() {
      this.isShowContextMenu = !this.isShowContextMenu;
    },
    /**
     * sự kiện contextmenu
     * Author: TTDuc (08/08/2022)
     */
    eventContextMenu() {
      event.preventDefault();
      this.toggleContextMenu();
      this.posTop = event.clientY;
      this.posLeft = event.clientX;
    },
    /**
     * format monney
     * Author: TTDuc (08/08/2022)
     */
    formatMoney(money) {
      if (!isNaN(money)) {
        return money.toString().replace(/(\d)(?=(\d{3})+(?:\.\d+)?$)/g, "$1.");
      } else {
        return money;
      }
    },
    /**
     * hàm chọn 1 item
     * Author: TTDuc (06/08/2022)
     */
    selectedItem(property) {
      this.currentProperty = property;
      if (!this.selectedProperties.includes(property)) {
        //thực hiện chọn
        this.selectedProperties.push(property);
        this.index = 0;
      } else {
        //thực hiện bỏ chọn
        this.selectedProperties = this.selectedProperties.filter(function (a) {
          return a !== property;
        });
      }
    },
    /**
     * hàm chọn tất cả item
     * Author: TTDuc (06/08/2022)
     */
    selectedAllItem() {
      if (this.selectedProperties.length < this.Properties.length) {
        this.selectedProperties = this.Properties;
      } else {
        this.selectedProperties = [];
      }
    },
    /**
     * hàm ẩn hiện Form FormDetail
     * Author: TTDuc (07/08/2022)
     */
    toggleFormDetail() {
      this.isShowDetail = !this.isShowDetail;
    },
    /**
     * hàm thêm mới TS
     * Author: TTDuc (07/08/2022)
     */
    addProperty() {
      //mở FormDetail
      this.toggleFormDetail();
      //validate

      //thực hiện lưu

      //thông báo thành công
    },
    /**
     * hàm click nextPage
     * Author: TTDuc (7/08/2022)
     */
    nextPage() {
      if (this.currentPage < this.maxPage) {
        this.currentPage++;
      }
    },
    /**
     * hàm click vào prevPage
     * Author: TTDuc (7/08/2022)
     */
    prevPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
    /**
     * hàm click vào 1 page number
     * Author: TTDuc (7/08/2022)
     */
    changeCurrentPage(selectedPage) {
      this.currentPage = selectedPage;
    },
    /**
     * hàm tính tổng của 1 prop trong mảng object
     * Author: TTDuc(08/08/2022)
     */
    total(array, propName) {
      let t = array.reduce(function (acc, cur) {
        return acc + cur[propName];
      }, 0);
      return t;
    },
  },
  computed: {},
};
</script>

<style scoped>
@import url(../css/main.css);
</style>
