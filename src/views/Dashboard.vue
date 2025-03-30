<template>
  <div>
    <el-button type="primary" class="me-2" data-bs-toggle="modal" data-bs-target="#kt_modal_new_data">Thêm mới data</el-button>
    <el-dropdown split-button type="primary" :disabled="!multipleSelection.length ? true : false">
      Gán nhân viên phụ trách data
      <template #dropdown>
        <el-dropdown-menu>
          <el-dropdown-item @click="openConfirm()">Nguyên Văn A</el-dropdown-item>
          <el-dropdown-item @click="openConfirm()">Nguyễn Thị B</el-dropdown-item>
          <el-dropdown-item @click="openConfirm()">Nguyễn Văn C</el-dropdown-item>
          <el-dropdown-item @click="openConfirm()">Nguyễn Văn D</el-dropdown-item>
        </el-dropdown-menu>
      </template>
    </el-dropdown>
    <el-table
      ref="multipleTableRef"
      :data="filterTableData"
      style="width: 100%"
      @selection-change="handleSelectionChange"
    >
      <el-table-column type="selection" width="55" />
      <el-table-column fixed="left" min-width="150" label="Mã data" prop="maData" />
      <el-table-column min-width="200" label="Tài khoản khách hàng" prop="taiKhoanKhachHang" />
      <el-table-column min-width="150" label="Tên khách hàng" prop="tenKhachHang" />
      <el-table-column min-width="150" label="Số điện thoại" prop="soDienThoai" />
      <el-table-column min-width="150" label="Ngành data" prop="nganhData" />
      <el-table-column min-width="150" label="Nguồn data" prop="nguonData" />
      <el-table-column min-width="150" label="Người phụ trách" prop="nguoiPhuTrach" />
      <el-table-column min-width="150" label="Logs chăm sóc" prop="logsChamSoc" />
      <el-table-column min-width="250" label="Nhân viên kinh doanh chính" prop="nvkdChinh" />
      <el-table-column min-width="200" label="Nhân viên kinh doanh phụ" prop="nvkdPhu" />
      <el-table-column min-width="200" label="Nhân viên chăm sóc" prop="nhanVienChamSoc" />
      <el-table-column min-width="100" label="Nhu cầu" prop="nhuCau" />
      <el-table-column min-width="100" label="Mã số thuế" prop="maSoThue" />
      <el-table-column min-width="150" label="Địa điểm công ty" prop="diaDiemCongTy" />
      <el-table-column min-width="150" label="Tên giám đốc" prop="tenGiamDoc" />
      <el-table-column min-width="200" label="Ngày sinh giám đốc" prop="ngaySinhGiamDoc" />
      <el-table-column min-width="200" label="Ngày sinh khách hàng" prop="ngaySinhKhachHang" />
      <el-table-column min-width="200" label="Địa điểm giao hàng" prop="diaDiemGiaoHang" />
      <el-table-column min-width="100" label="Tuổi nợ" prop="tuoiNo" />
      <el-table-column min-width="150" label="Hạn mức nợ" prop="hanMucNo" >
        <template #default="{ row }">
          {{ numberFormat(row.hanMucNo) }}
        </template>
      </el-table-column>
      <el-table-column min-width="100" label="Giám sát" prop="giamSat" />
      <el-table-column min-width="100" label="Nhóm zalo" prop="nhomZalo" />
      <el-table-column fixed="right" min-width="150" align="right">
        <template #header>
          <el-input v-model="search" size="small" placeholder="Tìm kiếm mã data" />
        </template>
        <template #default="scope">
          <el-button size="small" @click="handleEdit(scope.row)">
            Edit
          </el-button>
          <el-button
            size="small"
            type="danger"
            @click="handleDelete(scope.$index, scope.row)"
          >
            Delete
          </el-button>
        </template>
      </el-table-column>
    </el-table>
    <KTNewData></KTNewData>
  </div>
</template>

<script lang="ts" setup>
import { computed, ref } from "vue";
import KTNewData from "@/components/modals/forms/AddNewData.vue";
import { ElMessage, ElMessageBox } from 'element-plus'
import type { TableInstance } from 'element-plus'

interface tableData {
  maData: string,
  taiKhoanKhachHang: string,
  tenKhachHang: string,
  soDienThoai: string,
  nganhData: string,
  nguonData: string,
  nguoiPhuTrach: string,
  nhuCau: string,
  nhomZalo: string,
  logsChamSoc: string,
  maSoThue: string,
  diaDiemCongTy: string,
  tenGiamDoc: string,
  ngaySinhGiamDoc: string,
  ngaySinhKhachHang: string,
  diaDiemGiaoHang: string,
  tuoiNo: number,
  hanMucNo: number,
  nvkdChinh: string,
  nvkdPhu: string,
  nhanVienChamSoc: string,
  giamSat: string,
}

const search = ref("");
const multipleSelection = ref<tableData[]>([])
const multipleTableRef = ref<TableInstance>()
const filterTableData = computed(() =>
  tableData.filter(
    (data) =>
      !search.value ||
      data.maData.toLowerCase().includes(search.value.toLowerCase()),
  ),
);
const handleEdit = (row: tableData) => {
  console.log(row);
};
const handleDelete = (index: number, row: tableData) => {
  console.log(index, row);
};
function numberFormat(number: any, getDecimal: boolean = false) {
  if (!number) return "";
  number = String(number); // chuyển về string
  if (number.indexOf(".") === -1) {
    number += ".00";
  }
  var parts = number.split(".");
  var integerPart = parts[0];
  var decimalPart = parts[1];
  // thêm dấu ',' vào giữa các phần ngàn của phần số nguyên
  integerPart = integerPart.replace(/\B(?=(\d{3})+(?!\d))/g, ",");
  if ((!decimalPart || decimalPart === "00") && !getDecimal) {
    return integerPart;
  }
  return integerPart + "." + decimalPart;
}
const handleSelectionChange = (val: tableData[]) => {
  multipleSelection.value = val
}
const openConfirm = () => {
  ElMessageBox.confirm(
    'Bạn muốn gán nhân viên ... làm nhân viên phụ trách data?',
    'Warning',
    {
      confirmButtonText: 'Đồng ý',
      cancelButtonText: 'Hủy bỏ',
      type: 'warning',
    }
  )
    .then(() => {
      multipleTableRef.value!.clearSelection()
      ElMessage({
        type: 'success',
        message: 'Thành công!',
      })
    })
    .catch(() => {
      ElMessage({
        type: 'info',
        message: 'Không thành công!',
      })
    })
}

const tableData: tableData[] = [
  {
    maData: "DATA1",
    taiKhoanKhachHang: "hungleip9",
    tenKhachHang: "Lê Quang Hùng",
    soDienThoai: "0898562269",
    nganhData: "Thương mại",
    nguonData: "Shopee",
    nguoiPhuTrach: "nv1",
    nhuCau: "Mua xắm",
    nhomZalo: "Zalo vip 1",
    logsChamSoc: "",
    maSoThue: "1700",
    diaDiemCongTy: "115 - Bùi Thị Xuân",
    tenGiamDoc: "Lê Quang Châu",
    ngaySinhGiamDoc: "1/1/1997",
    ngaySinhKhachHang: "1/1/1998",
    diaDiemGiaoHang: "115 - Bùi Thị Xuân",
    tuoiNo: 1,
    hanMucNo: 20000000,
    nvkdChinh: "nv1",
    nvkdPhu: "nv2",
    nhanVienChamSoc: "",
    giamSat: "nv1",
  },
  {
    maData: "DATA2",
    taiKhoanKhachHang: "hungleip9",
    tenKhachHang: "Lê Quang Hùng",
    soDienThoai: "0898562269",
    nganhData: "Thương mại",
    nguonData: "Shopee",
    nguoiPhuTrach: "nv1",
    nhuCau: "Mua xắm",
    nhomZalo: "Zalo vip 1",
    logsChamSoc: "",
    maSoThue: "1700",
    diaDiemCongTy: "115 - Bùi Thị Xuân",
    tenGiamDoc: "Lê Quang Châu",
    ngaySinhGiamDoc: "1/1/1997",
    ngaySinhKhachHang: "1/1/1998",
    diaDiemGiaoHang: "115 - Bùi Thị Xuân",
    tuoiNo: 1,
    hanMucNo: 20000000,
    nvkdChinh: "nv1",
    nvkdPhu: "nv2",
    nhanVienChamSoc: "",
    giamSat: "nv1",
  },
  {
    maData: "DATA4",
    taiKhoanKhachHang: "hungleip9",
    tenKhachHang: "Lê Quang Hùng",
    soDienThoai: "0898562269",
    nganhData: "Thương mại",
    nguonData: "Shopee",
    nguoiPhuTrach: "nv1",
    nhuCau: "Mua xắm",
    nhomZalo: "Zalo vip 1",
    logsChamSoc: "",
    maSoThue: "1700",
    diaDiemCongTy: "115 - Bùi Thị Xuân",
    tenGiamDoc: "Lê Quang Châu",
    ngaySinhGiamDoc: "1/1/1997",
    ngaySinhKhachHang: "1/1/1998",
    diaDiemGiaoHang: "115 - Bùi Thị Xuân",
    tuoiNo: 1,
    hanMucNo: 20000000,
    nvkdChinh: "nv1",
    nvkdPhu: "nv2",
    nhanVienChamSoc: "",
    giamSat: "nv1",
  },
  {
    maData: "DATA3",
    taiKhoanKhachHang: "hungleip9",
    tenKhachHang: "Lê Quang Hùng",
    soDienThoai: "0898562269",
    nganhData: "Thương mại",
    nguonData: "Shopee",
    nguoiPhuTrach: "nv1",
    nhuCau: "Mua xắm",
    nhomZalo: "Zalo vip 1",
    logsChamSoc: "",
    maSoThue: "1700",
    diaDiemCongTy: "115 - Bùi Thị Xuân",
    tenGiamDoc: "Lê Quang Châu",
    ngaySinhGiamDoc: "1/1/1997",
    ngaySinhKhachHang: "1/1/1998",
    diaDiemGiaoHang: "115 - Bùi Thị Xuân",
    tuoiNo: 1,
    hanMucNo: 20000000,
    nvkdChinh: "nv1",
    nvkdPhu: "nv2",
    nhanVienChamSoc: "",
    giamSat: "nv1",
  },
];
</script>

<style scoped>
</style>
