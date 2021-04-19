<template>
  <div class="budget-list-wrap">
    <ElCard :header="header">
      <slot name="sort"></slot>
      <template v-if="!isEmpty">
        <slot></slot>
      </template>
      <ElAlert v-else type="info" :title="emptyTitle" :closable="false" />
    </ElCard>
  </div>
</template>

<script>

export default {
  name: "BudgetList",
  emits: [],
  props: {
    list: {
      type: Object,
      default: () => ({})
    }
  },
  data: () => ({
    header: "Budget List",
    emptyTitle: "Empty List"
  }),
  computed: {
    isEmpty() {
      return !Object.keys(this.list).length;
    }
  },
  methods: {
  },
  components: {
  }
};
</script>

<style scoped>
.budget-list-wrap {
  max-width: 500px;
  margin: auto;
}


</style>