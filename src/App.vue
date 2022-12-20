<template>
  <div id="app">
    <Form @submitForm="onFormSubmit" />
    <TotalBalance :total="totalBalance" />
    <BudgetList :list="list" />
  </div>
</template>

<script>
import BudgetList from "@/components/BudgetList";
import TotalBalance from "@/components/TotalBalance";
import Form from "@/components/Form";

export default {
  name: "App",
  components: {
    BudgetList,
    TotalBalance,
    Form,
  },
  data: () => ({
    list: {
      1: {
        type: "INCOME",
        value: 100,
        comment: "Some comment",
        id: 1,
      },
      2: {
        type: "EXPENSE",
        value: -50,
        comment: "Some expense",
        id: 2,
      },
    },
  }),
  computed: {
    totalBalance() {
      return Object.values(this.list).reduce(
        (acc, item) => acc + item.value,
        0
      );
    },
  },
  methods: {
    onFormSubmit(data) {
      const newObj = {
        ...data,
        id: String(Math.floor(Math.random() * 1000)),
      };
      this.$set(this.list, newObj.id, newObj);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
