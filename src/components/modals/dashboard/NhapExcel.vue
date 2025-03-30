<template>
  <div class="w-100 h-100">
    <el-button type="primary" class="mb-2" @click="downloadExcelDemo()">
      Tải file mẫu Excel<el-icon class="el-icon--right"><Download /></el-icon>
    </el-button>
    <el-upload
      drag
      :show-file-list="false"
      accept=".xlsx,.xls"
      :auto-upload="false"
      :on-change="handleFileChange"
      class="upload-demo mb-2"
    >
      <el-icon class="el-icon--upload"><upload-filled /></el-icon>
      <div class="el-upload__text">Thả file <em>chọn file upload</em></div>
    </el-upload>
    <p>{{ selectedFileName }}</p>
    <!-- table preview -->
    <el-table
      v-show="dataReview.length"
      :data="dataReview"
      style="width: 100%; max-height: 500px"
    >
      <el-table-column
        min-width="200"
        label="Tài khoản khách hàng"
        prop="taiKhoanKhachHang"
      />
      <el-table-column
        min-width="150"
        label="Tên khách hàng"
        prop="tenKhachHang"
      />
      <el-table-column
        min-width="150"
        label="Số điện thoại"
        prop="soDienThoai"
      />
      <el-table-column min-width="150" label="Ngành data" prop="nganhData" />
      <el-table-column min-width="150" label="Nguồn data" prop="nguonData" />
      <el-table-column
        min-width="150"
        label="Người phụ trách"
        prop="nguoiPhuTrach"
      />
      <el-table-column
        min-width="150"
        label="Logs chăm sóc"
        prop="logsChamSoc"
      />
      <el-table-column
        min-width="250"
        label="Nhân viên kinh doanh chính"
        prop="nvkdChinh"
      />
      <el-table-column
        min-width="200"
        label="Nhân viên kinh doanh phụ"
        prop="nvkdPhu"
      />
      <el-table-column
        min-width="200"
        label="Nhân viên chăm sóc"
        prop="nhanVienChamSoc"
      />
      <el-table-column min-width="100" label="Nhu cầu" prop="nhuCau" />
      <el-table-column min-width="100" label="Mã số thuế" prop="maSoThue" />
      <el-table-column
        min-width="150"
        label="Địa điểm công ty"
        prop="diaDiemCongTy"
      />
      <el-table-column min-width="150" label="Tên giám đốc" prop="tenGiamDoc" />
      <el-table-column
        min-width="200"
        label="Ngày sinh giám đốc"
        prop="ngaySinhGiamDoc"
      />
      <el-table-column
        min-width="200"
        label="Ngày sinh khách hàng"
        prop="ngaySinhKhachHang"
      />
      <el-table-column
        min-width="200"
        label="Địa điểm giao hàng"
        prop="diaDiemGiaoHang"
      />
      <el-table-column min-width="100" label="Tuổi nợ" prop="tuoiNo" />
      <el-table-column min-width="150" label="Hạn mức nợ" prop="hanMucNo" />
      <el-table-column min-width="100" label="Giám sát" prop="giamSat" />
      <el-table-column min-width="100" label="Nhóm zalo" prop="nhomZalo" />
    </el-table>
    <div
      class="w-100 d-flex justify-content-md-end mt-4"
      v-if="dataReview.length"
    >
      <el-button type="primary" @click="handleSaveDataForExcel()"
        >Lưu</el-button
      >
      <el-button @click="clearFile()">Clear file</el-button>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { reactive, ref, onBeforeMount } from "vue";
import { Download, UploadFilled } from "@element-plus/icons-vue";
import * as XLSX from "xlsx";
import headerMap from "@/core/data/dashboard";
import { ElMessage } from "element-plus";

const emit = defineEmits(['closeModal'])
const rules = ref<any>({});
const fileInputRef = ref();
const selectedFileName = ref('')
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
const framework = [
  { name: "George Washington", birthday: "1732-02-22" },
  { name: "John Adams", birthday: "1735-10-19" },
];
const dataReview = ref<any[]>([]);
onBeforeMount(() => {
  getRules();
});
const downloadExcelDemo = () => {
  const link = document.createElement("a");
  link.href = "/Demo-Data.xlsx"; // vì nó nằm trong public
  link.download = "DEMO_DATA.xlsx";
  link.click();
};
// const exportExcel = () => {
//   const XLSX = xlsx;
//   const workbook = XLSX.utils.book_new();
//   const worksheet = XLSX.utils.json_to_sheet(framework);
//   XLSX.utils.book_append_sheet(workbook, worksheet, "framework");
//   XLSX.writeFile(workbook, "framework.xlsx");
// };
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
const handleFileChange = (uploadFile) => {
  if (!uploadFile || !uploadFile.raw) {
    ElMessage({
      type: "error",
      message: "File không đúng định dạng!",
    });
    return
  }
  dataReview.value = []
  const file = uploadFile.raw || null
  selectedFileName.value = file.name || ''
  const reader = new FileReader()
  reader.readAsArrayBuffer(file)
  reader.onload = (e: any) => {
    const data = new Uint8Array(e.target.result)
    const workbook = XLSX.read(data, { type: 'array' })
    const sheetName = workbook.SheetNames[0]
    const worksheet = workbook.Sheets[sheetName]
    const jsonData = XLSX.utils.sheet_to_json(worksheet)
    if (!jsonData) {
      ElMessage({
        type: "error",
        message: "File không đúng định dạng!",
      });
      return;
    }
    dataReview.value = jsonData.map((row: any) => {
      const newRow = {};
      for (const key in row) {
        const newKey = headerMap[key] || key;
        newRow[newKey] = row[key];
      }
      return newRow;
    });
  }
}
const handleSaveDataForExcel = () => {
  ElMessage({
    type: 'success',
    message: 'Thêm data thành công!',
  })
  emit('closeModal')
};
const clearFile = () => {
  dataReview.value = [];
  selectedFileName.value = ''
  if (fileInputRef.value) {
    fileInputRef.value.value = "";
  }
};
</script>

<style lang="scss" scoped></style>
