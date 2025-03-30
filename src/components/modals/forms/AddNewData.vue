<template>
  <div
    class="modal fade"
    id="kt_modal_new_data"
    ref="newTargetModalRef"
    tabindex="-1"
    aria-hidden="true"
    data-bs-backdrop="static"
    data-bs-keyboard="false"
  >
    <div class="modal-dialog modal-dialog-centered">
      <div class="modal-content rounded">
        <div class="modal-header pb-0 border-0 justify-content-between">
          <div></div>
          <h1>Thêm data</h1>
          <div
            class="btn btn-sm btn-icon btn-active-color-primary"
            data-bs-dismiss="modal"
          >
            <KTIcon icon-name="cross" icon-class="fs-1" />
          </div>
        </div>

        <div class="modal-body scroll-y px-10 px-lg-15 pt-0 pb-15">
          <el-tabs v-model="activeName" class="demo-tabs">
            <el-tab-pane label="Nhập thủ công" name="thuCong">
              <el-form
                ref="ruleFormRef"
                :model="form"
                :rules="rules"
                class="form-container"
              >
                <el-row :gutter="20">
                  <!-- Cột trái -->
                  <el-col :xs="24" :sm="12">
                    <div class="d-flex flex-column mb-2 fv-row">
                      <label
                        class="d-flex align-items-center fs-6 fw-semibold mb-2"
                      >
                        <span class="required">Tài khoản khách hàng</span>
                      </label>
                      <el-form-item prop="taiKhoanKhachHang">
                        <el-input v-model="form.taiKhoanKhachHang" placeholder="Nhập tài khoản khách hàng" />
                      </el-form-item>
                    </div>

                    <div class="d-flex flex-column mb-2 fv-row">
                      <label
                        class="d-flex align-items-center fs-6 fw-semibold mb-2"
                      >
                        <span class="required">Tên khách hàng</span>
                      </label>
                      <el-form-item prop="tenKhachHang">
                        <el-input v-model="form.tenKhachHang" placeholder="Nhập tên khách hàng"/>
                      </el-form-item>
                    </div>

                    <div class="d-flex flex-column mb-2 fv-row">
                      <label
                        class="d-flex align-items-center fs-6 fw-semibold mb-2"
                      >
                        <span class="required">Số điện thoại</span>
                      </label>
                      <el-form-item prop="soDienThoai">
                        <el-input
                          v-model="form.soDienThoai"
                          placeholder="Nhập số điện thoại"
                          @input="
                            form.soDienThoai = form.soDienThoai.replace(
                              /[^0-9]/g,
                              '',
                            )
                          "
                        />
                      </el-form-item>
                    </div>

                    <div class="d-flex flex-column mb-2 fv-row">
                      <label
                        class="d-flex align-items-center fs-6 fw-semibold mb-2"
                      >
                        <span>Ngành Data</span>
                      </label>
                      <el-form-item prop="nganhData">
                        <el-input v-model="form.nganhData" placeholder="Nhập ngành data"/>
                      </el-form-item>
                    </div>

                    <div class="d-flex flex-column mb-2 fv-row">
                      <label
                        class="d-flex align-items-center fs-6 fw-semibold mb-2"
                      >
                        <span>Nguồn Data</span>
                      </label>
                      <el-form-item prop="nguonData">
                        <el-input v-model="form.nguonData" placeholder="Nhập nguồn data"/>
                      </el-form-item>
                    </div>

                    <div class="d-flex flex-column mb-2 fv-row">
                      <label
                        class="d-flex align-items-center fs-6 fw-semibold mb-2"
                      >
                        <span>Người phụ trách</span>
                      </label>
                      <el-form-item prop="nguoiPhuTrach">
                        <el-select
                          v-model="form.nguoiPhuTrach"
                          placeholder="Chọn nhân viên"
                          style="width: 100%"
                        >
                          <el-option label="Nguyễn Văn A" value="nv1" />
                          <el-option label="Trần Thị B" value="nv2" />
                        </el-select>
                      </el-form-item>
                    </div>

                    <div class="d-flex flex-column mb-2 fv-row">
                      <label
                        class="d-flex align-items-center fs-6 fw-semibold mb-2"
                      >
                        <span>NVKD chính</span>
                      </label>
                      <el-form-item prop="nvkdChinh">
                        <el-select
                          v-model="form.nvkdChinh"
                          placeholder="Chọn nhân viên"
                          style="width: 100%"
                        >
                          <el-option label="Nguyễn Văn A" value="nv1" />
                          <el-option label="Trần Thị B" value="nv2" />
                        </el-select>
                      </el-form-item>
                    </div>

                    <div class="d-flex flex-column mb-2 fv-row">
                      <label
                        class="d-flex align-items-center fs-6 fw-semibold mb-2"
                      >
                        <span>NVKD phụ</span>
                      </label>
                      <el-form-item prop="nvkdPhu">
                        <el-select
                          v-model="form.nvkdPhu"
                          placeholder="Chọn nhân viên"
                          style="width: 100%"
                        >
                          <el-option label="Nguyễn Văn A" value="nv1" />
                          <el-option label="Trần Thị B" value="nv2" />
                        </el-select>
                      </el-form-item>
                    </div>

                    <div class="d-flex">
                      <div class="d-flex flex-column mb-2 me-2 fv-row">
                        <label
                          class="d-flex align-items-center fs-6 fw-semibold mb-2"
                        >
                          <span>Tuổi nợ (ngày)</span>
                        </label>
                        <el-form-item prop="tuoiNo">
                          <el-input-number v-model="form.tuoiNo" placeholder="Nhập tuổi nợ" />
                        </el-form-item>
                      </div>
  
                      <div class="d-flex flex-column mb-2 fv-row">
                        <label
                          class="d-flex align-items-center fs-6 fw-semibold mb-2"
                        >
                          <span>Hạn mức nợ</span>
                        </label>
                        <el-form-item prop="hanMucNo">
                          <el-input-number v-model="form.hanMucNo" placeholder="Nhập hạn mức nợ"/>
                        </el-form-item>
                      </div>
                    </div>
                  </el-col>

                  <!-- Cột phải -->
                  <el-col :xs="24" :sm="12">
                    <div class="d-flex flex-column mb-2 fv-row">
                      <label
                        class="d-flex align-items-center fs-6 fw-semibold mb-2"
                      >
                        <span>Nhân viên chăm sóc</span>
                      </label>
                      <el-form-item prop="nhanVienChamSoc">
                        <el-select
                          v-model="form.nhanVienChamSoc"
                          placeholder="Chọn nhân viên"
                          style="width: 100%"
                        >
                          <el-option label="Nguyễn Văn A" value="nv1" />
                          <el-option label="Trần Thị B" value="nv2" />
                        </el-select>
                      </el-form-item>
                    </div>

                    <div
                      class="d-flex flex-column mb-2 fv-row"
                      v-for="field in [
                        { label: 'Mã số thuế', prop: 'maSoThue' },
                        { label: 'Địa điểm công ty', prop: 'diaDiemCongTy' },
                        { label: 'Tên giám đốc', prop: 'tenGiamDoc' },
                        {
                          label: 'Ngày sinh Giám đốc',
                          prop: 'ngaySinhGiamDoc',
                          type: 'date',
                        },
                        {
                          label: 'Ngày sinh khách hàng',
                          prop: 'ngaySinhKhachHang',
                          type: 'date',
                        },
                        {
                          label: 'Địa điểm giao hàng',
                          prop: 'diaDiemGiaoHang',
                        },
                        { label: 'Người giám sát', prop: 'giamSat' },
                        { label: 'Nhóm ZALO', prop: 'nhomZalo' },
                      ]"
                      :key="field.prop"
                    >
                      <label
                        class="d-flex align-items-center fs-6 fw-semibold mb-2"
                      >
                        <span>{{ field.label }}</span>
                      </label>
                      <el-form-item :prop="field.prop">
                        <component
                          :is="
                            field.type === 'date'
                              ? 'el-date-picker'
                              : field.type === 'number'
                                ? 'el-input-number'
                                : 'el-input'
                          "
                          v-model="form[field.prop]"
                          :type="field.type"
                          style="width: 100%"
                          format="DD/MM/YYYY"
                          :placeholder="`Nhập ${field.label.toLowerCase()}`"
                          :min="field.type === 'number' ? 0 : undefined"
                        />
                      </el-form-item>
                    </div>
                  </el-col>
                </el-row>

                <!-- Các phần toàn dòng -->
                <div
                  class="d-flex flex-column mb-2 fv-row">
                  <label
                    class="d-flex align-items-center fs-6 fw-semibold mb-2"
                  >
                    <span>Nhu cầu quan tâm</span>
                  </label>
                  <el-form-item prop="nhuCau">
                    <el-input
                      v-model="form.nhuCau"
                      type="textarea"
                      rows="2"
                      placeholder="Nhập nhu cầu quan tâm"
                    />
                  </el-form-item>
                </div>
                
                <div
                  class="d-flex flex-column mb-2 fv-row">
                  <label
                    class="d-flex align-items-center fs-6 fw-semibold mb-2"
                  >
                    <span>Logs chăm sóc</span>
                  </label>
                  <el-form-item prop="logsChamSoc">
                    <el-input
                      v-model="form.logsChamSoc"
                      type="textarea"
                      rows="3"
                      placeholder="Nhập logs chăm sóc"
                    />
                  </el-form-item>
                </div>
                <!-- action -->
                <el-form-item>
                  <div class="w-100 d-flex justify-content-md-end">
                    <el-button type="primary" @click="submitForm(ruleFormRef)">Tạo mới</el-button>
                    <el-button @click="resetForm(ruleFormRef)">Reset form</el-button>
                  </div>
                </el-form-item>
                
              </el-form>
            </el-tab-pane>
            <el-tab-pane label="Nhập theo excel" name="excel"
              >Nhập theo Excel
            </el-tab-pane>
          </el-tabs>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { reactive, ref, onBeforeMount } from "vue";
import type { FormInstance, TabsPaneContext } from "element-plus";

const ruleFormRef = ref<FormInstance>();
const rules = ref<any>({});
const activeName = ref("thuCong");
const form = reactive({
  maData: "",
  taiKhoanKhachHang: "",
  tenKhachHang: "",
  soDienThoai: "",
  nganhData: "",
  nguonData: "",
  nguoiPhuTrach: "",
  nhuCau: "",
  nhomZalo: "",
  logsChamSoc: "",
  maSoThue: "",
  diaDiemCongTy: "",
  tenGiamDoc: "",
  ngaySinhGiamDoc: "",
  ngaySinhKhachHang: "",
  diaDiemGiaoHang: "",
  tuoiNo: 0,
  hanMucNo: 0,
  nvkdChinh: "",
  nvkdPhu: "",
  nhanVienChamSoc: "",
  giamSat: "",
});
onBeforeMount(() => {
  getRules();
});

const getRules = () => {
  Object.keys(form).forEach((key) => {
    const arrRule = [
      {
        required: false,
      },
    ];
    rules.value[key] = arrRule;
  });
  rules.value.taiKhoanKhachHang = [
    {
      required: true,
      message: "Bạn chưa nhập tài khoản khách hàng!",
      trigger: "change",
    },
  ];
  rules.value.tenKhachHang = [
    {
      required: true,
      message: "Bạn chưa nhập tên khách hàng!",
      trigger: "change",
    },
  ];
  rules.value.soDienThoai = [
    {
      required: true,
      message: "Bạn chưa nhập số điện thoại!",
      trigger: "change",
    },
  ];
};
const submitForm = async (formEl: FormInstance | undefined) => {
  if (!formEl) return;
  await formEl.validate((valid, fields) => {
    if (valid) {
      console.log("submit!");
    } else {
      console.log("error submit!", fields);
    }
  });
};
const handleClose = (ruleFormRef: FormInstance | undefined) => {
  resetForm(ruleFormRef)
}
const resetForm = (formEl: FormInstance | undefined) => {
  if (!formEl) return;
  formEl.resetFields();
};
</script>

<style lang="scss">
.modal-dialog {
  max-width: 90vw;
  .modal-content {
    .modal-body {
      height: 80vh;
    }
  }
}
.override-styles {
  z-index: 99999 !important;
  pointer-events: initial;
}
.el-select {
  width: 100%;
}

.el-date-editor.el-input,
.el-date-editor.el-input__inner {
  width: 100%;
}
.form-container {
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
}
</style>
