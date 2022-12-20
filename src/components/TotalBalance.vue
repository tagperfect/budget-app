<template>
  <div class="total-value" :class="[classObj]">Balance: {{ total }}</div>
</template>

<script>
export default {
  name: "TotalBalance",
  props: {
    total: {
      type: Number,
      default: 0,
    },
  },
  computed: {
    classObj() {
      return {
        green: this.total > 0 ? true : false,
        red: this.total < 0 ? true : false,
      };
    },
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
.green{
  color: green;
}
.red{
  color: red
}
</style>