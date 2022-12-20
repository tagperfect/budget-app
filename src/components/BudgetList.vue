<template>
  <div class="budget-list-wrap">
    <div class="expense-actions">
      <ElButton
        type="info"
        size="mini"
        @click="filterList('INCOME')"
        icon="el-icon-top"
        >Show Income</ElButton
      >
      <ElButton
        type="info"
        size="mini"
        @click="filterList('EXPENSE')"
        icon="el-icon-bottom"
        >Show Expense</ElButton
      >
      <ElButton
        type="info"
        size="mini"
        @click="filterList('ALL')"
        icon="el-icon-close"
        >Show Both</ElButton
      >
    </div>

    <ElCard :header="header">
      <template v-if="!isEmpty">
        <BudgetListItem
          v-for="(item, prop) in filteredList"
          :key="prop"
          :item="item"
          @deleteItem="onDeleteItem"
        />
      </template>
      <ElAlert v-else type="info" :title="emptyTitle" :closable="false" />
    </ElCard>
  </div>
</template>

<script>
import BudgetListItem from "@/components/BudgetListItem";

export default {
  name: "BudgetList",
  components: {
    BudgetListItem,
  },
  props: {
    list: {
      type: Object,
      default: () => ({}),
    },
  },
  data: () => ({
    header: "Budget List",
    emptyTitle: "Empty List",
    dialogVisible: false,
    filteredList: {},
  }),
  created() {
    this.filterList("ALL");
  },
  computed: {
    isEmpty() {
      return !Object.keys(this.list).length;
    },
  },
  methods: {
    onDeleteItem(id) {
      this.dialogVisible = true;
      this.$delete(this.list, id);
    },
    filterList(type) {
      const listArr = Object.values(this.list);
      if (type === "ALL") {
        this.filteredList = this.list;
      } else {
        this.filteredList = listArr.filter((item) => item.type === type);
      }
    },
  },
};
</script>

<style scoped>
.budget-list-wrap {
  max-width: 500px;
  margin: auto;
}
.expense-actions {
  padding-bottom: 20px;
}
</style>