<template>
  <div id="form-detail" class="popup" v-if="isShow">
    <div class="form-detail__container">
      <div class="form-detail__header">
        <div class="form-detail__text">
          <h2>Thêm tài sản</h2>
        </div>
        <div @click="closeForm" class="form-detail__close">
          <div class="icon">
            <div class="icon-close"></div>
          </div>
        </div>
      </div>
      <div class="form-detail__content">
        <div class="row">
          <label for="">Mã tài sản <span>*</span></label>
          <div class="form-input">
            <input class="input" type="text" tabindex="1" id="inputFocus" @blur="validate" />
          </div>
        </div>

        <div class="row col-2">
          <label for="">Tên tài sản <span>*</span></label>
          <div class="form-input">
            <input class="input" type="text" placeholder="Nhập tên tài sản" tabindex="2" />
          </div>
        </div>
        <div class="row">
          <label for="">Mã bộ phận sử dụng <span>*</span></label>
          <m-combobox-2 class="combobox" tabindex="3" />
        </div>
        <div class="row col-2">
          <label for="">Tên bộ phận sử dụng</label>
          <div class="form-input">
            <input class="input" type="text" readonly="" fieldname="UserName" />
          </div>
        </div>
        <div class="row">
          <label for="">Mã bộ phận sử dụng <span>*</span></label>
          <m-combobox-2 class="combobox" tabindex="4" />
        </div>
        <div class="row col-2">
          <label for="">Tên loại tài sản</label>
          <div class="form-input">
            <input class="input" type="text" readonly="" />
          </div>
        </div>
        <div class="row">
          <label for="">Số lượng <span>*</span></label>
          <div class="form-input input-number">
            <input class="input text-right" type="text" datatype="number" tabindex="5" fieldname="Quantity"
              required="" />
            <div class="up-down">
              <div class="up">
                <div class="btn icon-up__black"></div>
              </div>
              <div class="down">
                <div class="btn icon-down__black"></div>
              </div>
            </div>
          </div>
        </div>
        <div class="row">
          <label for="">Nguyên giá <span>*</span></label>
          <div class="form-input">
            <input class="input text-right" value="0" datatype="number" tabindex="6" fieldname="Price" required="" />
          </div>
        </div>
        <div class="row">
          <label for="">Số năm sử dụng</label>
          <div class="form-input">
            <input class="input text-right" type="text" datatype="number" tabindex="6" fieldname="UsedYear"
              required="" />
          </div>
        </div>

        <div class="row">
          <label for="">Tỷ lệ hao mòn(%) <span>*</span></label>
          <div class="form-input input-number">
            <input class="input text-right" type="text" datatype="number" tabindex="7" fieldname="WearRate"
              required="" />
            <div class="up-down">
              <div class="up">
                <div class="btn icon-up__black"></div>
              </div>
              <div class="down">
                <div class="btn icon-down__black"></div>
              </div>
            </div>
          </div>
        </div>
        <div class="row">
          <label for="">Giá trị hao mòn <span>*</span></label>
          <div class="form-input">
            <input class="input text-right .asd" value="0" type="text" datatype="number" tabindex="8"
              fieldname="ValueWear" required="" />
          </div>
        </div>
        <div class="row">
          <label for="">Năm theo dõi</label>
          <div class="form-input">
            <input class="input text-right" type="text" readonly="" datatype="number" fieldname="YearFollow" />
          </div>
        </div>
        <div class="row">
          <label for="">Ngày mua <span>*</span></label>
          <div class="form-input">
            <input class="input" type="date" tabindex="9" fieldname="BuyDate" required="" />
          </div>
        </div>
        <div class="row">
          <label for="">Ngày bắt đầu sử dụng <span>*</span></label>
          <div class="form-input">
            <input class="input" type="date" tabindex="10" fieldname="StartUsingDate" required="" />
          </div>
        </div>
      </div>
      <div class="form-detail__controler">
        <button class="button button__close" tabindex="11">hủy</button>
        <button class="button button__save" tabindex="12">lưu</button>
      </div>
    </div>
  </div>
</template>

<script>
import MCombobox2 from "./MCombobox2.vue";

export default {
  components: {
    MCombobox2,
  },
  props: {
    isShow: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {};
  },
  methods: {
    /**
     * validate 
     * Author : TTDuc (10/08/2022)
     */
    validate(e) {
      console.log(e.target === this.$el.querySelector('.asd'));
      console.log(this.$el.querySelectorAll("input")[3]);
    },
    /**
     * hàm đóng form
     * Author: TTDuc (07/08/2022)
     */
    closeForm() {
      this.$emit("closeForm");
    },
  },
  updated() {
    if (this.$el.querySelector("#inputFocus")) {
      this.$el.querySelector("#inputFocus").focus();
    }
  },
};
</script>
