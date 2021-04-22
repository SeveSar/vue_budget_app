<template>
  <el-dialog
    title="Notice"
    v-model="centerDialogVisible"
    width="30%"
    center
    :close-on-click-modal="false"
    :show-close="false">
    <span>Notice: Do you really wanna delete this item?</span>
    <template #footer>
      <span class="dialog-footer">
        <el-button @click="cancelPop">Cancel</el-button>
        <el-button type="primary" @click="confirmPop">Confirm</el-button>
      </span>
      <div class="checkbox">
        <el-checkbox v-model="checked">Dont show this message again</el-checkbox>
        </div>
    </template>
  </el-dialog>
</template>
<script>
export default {
  props: ['visible'],
  emits: ['confirm-del', 'cancel-del'],
   data() {
      return {
        centerDialogVisible: false,
        checked: false
      };
  },
  methods: {
    cancelPop() {
      this.$emit('cancel-del')
      this.checked = false
    },
    confirmPop() {
      this.$emit('confirm-del', this.checked)
    },
  },
  watch: {
    visible (value) {
      if (value === true) {
        this.centerDialogVisible = value
      } else if(value === false) {
        this.centerDialogVisible = value
      }
    },
  }
};
</script>
<style lang="css">
.el-dialog__body {
  text-transform: uppercase;
  text-align: center !important;
}
.checkbox {
  margin-top: 20px;
}
</style>