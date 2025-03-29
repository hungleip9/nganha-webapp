<template>
  <el-form :model="form" label-width="180px" class="form-container">
    <el-row :gutter="20">
      <!-- Cột trái -->
      <el-col :xs="24" :sm="12">
        <el-form-item label="Mã Data (tự sinh)">
          <el-input v-model="form.maData" disabled />
        </el-form-item>

        <el-form-item label="Tài khoản khách hàng">
          <el-input v-model="form.taiKhoanKH" />
        </el-form-item>

        <el-form-item label="Tên khách hàng">
          <el-input v-model="form.tenKH" />
        </el-form-item>

        <el-form-item label="Số điện thoại">
          <el-input
            v-model="form.soDienThoai"
            @input="form.soDienThoai = form.soDienThoai.replace(/[^0-9]/g, '')"
          />
        </el-form-item>

        <el-form-item label="Ngành Data">
          <el-input v-model="form.nganhData" />
        </el-form-item>

        <el-form-item label="Nguồn Data">
          <el-input v-model="form.nguonData" />
        </el-form-item>

        <el-form-item label="Người phụ trách">
          <el-input v-model="form.nguoiPhuTrach" />
        </el-form-item>

        <el-form-item label="Loại khách hàng">
          <el-select
            v-model="form.loaiKH"
            placeholder="Chọn loại khách hàng"
            style="width: 100%"
          >
            <el-option label="Data" value="data" />
            <el-option label="Loại 3 - Có báo giá" value="loai3" />
            <el-option label="Loại 2 - Ký HĐ nguyên tắc" value="loai2" />
            <el-option label="Loại 1 - Có đơn hàng" value="loai1" />
          </el-select>
        </el-form-item>

        <el-form-item label="Mã khách hàng">
          <el-input v-model="form.maKhachHang" />
        </el-form-item>

        <el-form-item label="NVKD chính">
          <el-input v-model="form.nvkdChinh" />
        </el-form-item>

        <el-form-item label="NVKD phụ">
          <el-input v-model="form.nvkdPhu" />
        </el-form-item>

        <el-form-item label="Đính kèm HĐ nguyên tắc">
          <el-upload
            action="#"
            :auto-upload="false"
            :limit="1"
            :on-change="handleContractChange"
          >
            <el-button type="primary">Tải lên hợp đồng</el-button>
          </el-upload>
        </el-form-item>

        <el-form-item label="Đính kèm CCCD / GPKD">
          <el-upload
            action="#"
            :auto-upload="false"
            :limit="5"
            multiple
            :on-change="handleCCCDChange"
          >
            <el-button type="primary">Tải lên tài liệu</el-button>
          </el-upload>
        </el-form-item>
      </el-col>

      <!-- Cột phải -->
      <el-col :xs="24" :sm="12">
        <el-form-item label="Gán CSKH">
          <el-select
            v-model="form.nhanVienChamSoc"
            multiple
            placeholder="Chọn nhân viên"
            style="width: 100%"
          >
            <el-option label="Nguyễn Văn A" value="nv1" />
            <el-option label="Trần Thị B" value="nv2" />
          </el-select>
        </el-form-item>

        <el-form-item label="Mã số thuế">
          <el-input v-model="form.maSoThue" />
        </el-form-item>

        <el-form-item label="Địa điểm công ty">
          <el-input v-model="form.diaDiemCongTy" />
        </el-form-item>

        <el-form-item label="Tên giám đốc">
          <el-input v-model="form.tenGiamDoc" />
        </el-form-item>

        <el-form-item label="Ngày sinh Giám đốc">
          <el-date-picker
            v-model="form.ngaySinhGiamDoc"
            type="date"
            style="width: 100%"
          />
        </el-form-item>

        <el-form-item label="Ngày sinh khách hàng">
          <el-date-picker
            v-model="form.ngaySinhKH"
            type="date"
            style="width: 100%"
          />
        </el-form-item>

        <el-form-item label="Địa điểm giao hàng">
          <el-input v-model="form.diaDiemGiaoHang" />
        </el-form-item>

        <el-form-item label="Tuổi nợ (ngày)">
          <el-input-number v-model="form.tuoiNo" :min="0" style="width: 100%" />
        </el-form-item>

        <el-form-item label="Hạn mức nợ">
          <el-input-number
            v-model="form.hanMucNo"
            :min="0"
            style="width: 100%"
          />
        </el-form-item>

        <el-form-item label="Người giám sát">
          <el-input v-model="form.giamSat" />
        </el-form-item>

        <el-form-item label="Nhóm ZALO">
          <el-input v-model="form.nhomZalo" />
        </el-form-item>

        <el-form-item label="Mã đơn hàng">
          <el-input v-model="form.donHang" />
        </el-form-item>
      </el-col>
    </el-row>

    <!-- Các phần toàn dòng -->
    <el-form-item label="Logs chăm sóc">
      <el-input v-model="form.logsChamSoc" type="textarea" rows="3" />
    </el-form-item>

    <el-form-item label="Nhu cầu quan tâm">
      <el-input v-model="form.nhuCau" type="textarea" rows="2" />
    </el-form-item>

    <el-form-item label="Log đánh giá / góp ý / claim">
      <el-input v-model="form.logDanhGia" type="textarea" rows="2" />
    </el-form-item>

    <!-- Nút hành động -->
    <el-form-item>
      <el-button type="primary" @click="onSubmit">Tạo mới</el-button>
      <el-button>Huỷ</el-button>
    </el-form-item>
  </el-form>
</template>

<script lang="ts" setup>
import { reactive } from "vue";

const form = reactive({
  maData: "DATA123456",
  taiKhoanKH: "",
  tenKH: "",
  soDienThoai: "",
  nganhData: "",
  nguonData: "",
  nguoiPhuTrach: "",
  logsChamSoc: "",
  loaiKH: "",
  maKhachHang: "",
  nvkdChinh: "",
  nvkdPhu: "",
  nhanVienChamSoc: [],
  nhuCau: "",
  maSoThue: "",
  diaDiemCongTy: "",
  tenGiamDoc: "",
  ngaySinhGiamDoc: "",
  ngaySinhKH: "",
  diaDiemGiaoHang: "",
  tuoiNo: 0,
  hanMucNo: 0,
  giamSat: "",
  nhomZalo: "",
  donHang: "",
  logDanhGia: "",
});

const handleContractChange = (file: any) => {
  console.log("Hợp đồng:", file.name);
};
const handleCCCDChange = (file: any) => {
  console.log("Tài liệu CCCD/GPKD:", file.name);
};
const onSubmit = () => {
  console.log("Form dữ liệu:", form);
};
</script>

<style scoped>
.form-container {
  padding: 20px;
  background-color: #fff;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
}
</style>
