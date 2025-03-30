<template>
  <el-dialog v-model="dialogVisible"
    :modal="false"
    width="70%"
    :close-on-click-modal="false">
    <el-tabs v-model="activeName" class="demo-tabs overflow-hidden h-100">
      <div class="tab-pane">
        <el-tab-pane label="Nhập thủ công" name="thuCong">
          <KTNhapThuCong @closeModal="closeModal"/>
        </el-tab-pane>
        <el-tab-pane label="Nhập theo excel" name="excel">
          <KTNhapExcel @closeModal="closeModal"/>
        </el-tab-pane>
      </div>
    </el-tabs>
  </el-dialog>
  <!-- <div
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

        <div class="modal-body px-10 px-lg-15 pt-0 pb-15">
          <el-tabs
            v-model="activeName"
            class="demo-tabs overflow-hidden h-100"
          >
            <div class="tab-pane">
              <el-tab-pane label="Nhập thủ công" name="thuCong">
                <KTNhapThuCong />
              </el-tab-pane>
              <el-tab-pane label="Nhập theo excel" name="excel">
                <KTNhapExcel />
              </el-tab-pane>
            </div>
          </el-tabs>
          <div @click="closeModal()">aaaa</div>
        </div>
      </div>
    </div>
  </div> -->
</template>

<script lang="ts" setup>
import { ref } from "vue";
import KTNhapThuCong from "@/components/modals/dashboard/NhapThuCong.vue";
import KTNhapExcel from "@/components/modals/dashboard/NhapExcel.vue";
const activeName = ref("thuCong");
const dialogVisible = ref(false);
const openModal = () => {
  dialogVisible.value = true;
};
const closeModal = () => {
  dialogVisible.value = false;
};
defineExpose({
  openModal,
  closeModal,
});
</script>

<style lang="scss">
.el-dialog {
  height: 80vh;
  margin: 10vh auto!important;
  .el-dialog__body {
    height: 90%;
  }
}
.el-tabs__content {
  height: 100%;
  .tab-pane {
    height: 95%;
    overflow-y: auto;
  }
}
</style>
