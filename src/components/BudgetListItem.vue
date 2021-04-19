<template lang="">
   <div class="list-item">
      <span class="budget-comment">{{ item_data.comment }}</span>
      <span class="budget-value" :style="{color: checkType ? 'green' : 'red'}"><i :class="checkType ? 'el-icon-top' : 'el-icon-bottom'"></i> {{ item_data.value }}</span>
      <el-button type="danger" size="mini" @click="mark(item_data.id)"><i class="el-icon-delete"></i> Delete</el-button>
    </div>
</template>
<script>
export default {
  components: {
  },
  data() {
    return {
    }
  },
  emits: ['mark'],
  props: {
    item_data: {
      type: Object,
      default: () => ({}),
    }
  },
  methods: {
    mark (id) {
      this.$emit('mark',id)
    }
  },
  computed: {
    checkType () {
      return this.item_data.type === 'INCOME'
    }
  }
}
</script>
<style lang="css">
.list-item {
  display: flex;
  align-items: center;
  padding: 10px 15px;
}
.budget-value {
  font-weight: bold;
  margin-left: auto;
  margin-right: 20px;
}
</style>