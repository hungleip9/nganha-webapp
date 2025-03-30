<template>
  <div class="w-100 h-100">
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
            <label class="d-flex align-items-center fs-6 fw-semibold mb-2">
              <span class="required">Tài khoản khách hàng</span>
            </label>
            <el-form-item prop="taiKhoanKhachHang">
              <el-input
                v-model="form.taiKhoanKhachHang"
                placeholder="Nhập tài khoản khách hàng"
              />
            </el-form-item>
          </div>

          <div class="d-flex flex-column mb-2 fv-row">
            <label class="d-flex align-items-center fs-6 fw-semibold mb-2">
              <span class="required">Tên khách hàng</span>
            </label>
            <el-form-item prop="tenKhachHang">
              <el-input
                v-model="form.tenKhachHang"
                placeholder="Nhập tên khách hàng"
              />
            </el-form-item>
          </div>

          <div class="d-flex flex-column mb-2 fv-row">
            <label class="d-flex align-items-center fs-6 fw-semibold mb-2">
              <span class="required">Số điện thoại</span>
            </label>
            <el-form-item prop="soDienThoai">
              <el-input
                v-model="form.soDienThoai"
                placeholder="Nhập số điện thoại"
                @input="
                  form.soDienThoai = form.soDienThoai.replace(/[^0-9]/g, '')
                "
              />
            </el-form-item>
          </div>

          <div class="d-flex flex-column mb-2 fv-row">
            <label class="d-flex align-items-center fs-6 fw-semibold mb-2">
              <span>Ngành Data</span>
            </label>
            <el-form-item prop="nganhData">
              <el-input
                v-model="form.nganhData"
                placeholder="Nhập ngành data"
              />
            </el-form-item>
          </div>

          <div class="d-flex flex-column mb-2 fv-row">
            <label class="d-flex align-items-center fs-6 fw-semibold mb-2">
              <span>Nguồn Data</span>
            </label>
            <el-form-item prop="nguonData">
              <el-input
                v-model="form.nguonData"
                placeholder="Nhập nguồn data"
              />
            </el-form-item>
          </div>

          <div class="d-flex flex-column mb-2 fv-row">
            <label class="d-flex align-items-center fs-6 fw-semibold mb-2">
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
            <label class="d-flex align-items-center fs-6 fw-semibold mb-2">
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
            <label class="d-flex align-items-center fs-6 fw-semibold mb-2">
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
              <label class="d-flex align-items-center fs-6 fw-semibold mb-2">
                <span>Tuổi nợ (ngày)</span>
              </label>
              <el-form-item prop="tuoiNo">
                <el-input-number
                  v-model="form.tuoiNo"
                  placeholder="Nhập tuổi nợ"
                />
              </el-form-item>
            </div>

            <div class="d-flex flex-column mb-2 fv-row">
              <label class="d-flex align-items-center fs-6 fw-semibold mb-2">
                <span>Hạn mức nợ</span>
              </label>
              <el-form-item prop="hanMucNo">
                <el-input-number
                  v-model="form.hanMucNo"
                  placeholder="Nhập hạn mức nợ"
                />
              </el-form-item>
            </div>
          </div>
        </el-col>

        <!-- Cột phải -->
        <el-col :xs="24" :sm="12">
          <div class="d-flex flex-column mb-2 fv-row">
            <label class="d-flex align-items-center fs-6 fw-semibold mb-2">
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
            <label class="d-flex align-items-center fs-6 fw-semibold mb-2">
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
      <div class="d-flex flex-column mb-2 fv-row">
        <label class="d-flex align-items-center fs-6 fw-semibold mb-2">
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

      <div class="d-flex flex-column mb-2 fv-row">
        <label class="d-flex align-items-center fs-6 fw-semibold mb-2">
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
          <el-button type="primary" @click="submitForm(ruleFormRef)"
            >Tạo mới</el-button
          >
          <el-button @click="resetForm(ruleFormRef)">Reset form</el-button>
        </div>
      </el-form-item>
    </el-form>
  </div>
</template>

<script lang="ts" setup>
import { reactive, ref, onBeforeMount } from "vue";
import type { FormInstance } from "element-plus";
import { ElMessage } from "element-plus";

const emit = defineEmits(['closeModal'])

const rules = ref<any>({});
const ruleFormRef = ref<FormInstance>();
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
    if (!valid) {
      console.log("error submit!", fields);
      ElMessage({
        type: "error",
        message: "Thêm data thất bại!",
      });
      return
    }
    console.log('form: ', form);
    ElMessage({
      type: 'success',
      message: 'Thêm data thành công!',
    })
    emit('closeModal')
  });
};
const resetForm = (formEl: FormInstance | undefined) => {
  if (!formEl) return;
  formEl.resetFields();
};
</script>
