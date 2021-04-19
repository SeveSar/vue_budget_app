<template lang="">
  <div class="sort-btns">
    <el-button :type="type" v-for="(type, value, index) of btnType" :key="type" @click="$emit(`${clickActions[index]}`)">{{value}}</el-button>
  </div>
</template>
<script>
export default {
  emits: ['income-sort', 'outcome-sort', 'all-sort'],
  data () {
    return {
      btnType: {
        'Income': 'success',
        'Outcome': 'danger',
        'All': 'primary'
      },
      clickActions: ['income-sort', 'outcome-sort', 'all-sort'],
    }
  },
  methods: {
  },

}
</script>
<style lang="css" scoped>
.sort-btns {
  margin-top: 30px;
  margin-bottom: 30px;
}
.el-button {
  min-width: 100px;
}
</style>