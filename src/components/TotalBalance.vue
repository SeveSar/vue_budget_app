<template>
  <div class="total-value" :style="[checkZeroTotal ? {color: 'black'} : {color: total > 0 ? 'green': 'red'}]">Balance: {{ total }}</div>
</template>

<script>
export default {
  name: "TotalBalance",
  props: {
    total: {
      type: Number,
      default: 0
    }
  },
  computed: {
    checkZeroTotal () {
      return this.total === 0
    }
  }
};
</script>

<style scoped>
.total-value {
  font-size: 26px;
  text-transform: uppercase;
  padding: 20px;
  text-align: center;
}
</style>