<template>
  <div class="list-item">
    <span class="budget-comment"
      ><i :class="[classIcon, classObj]"></i> {{ item.comment }}</span
    >
    <span class="budget-value" :class="[classObj]">{{ item.value }}</span>
    <ElButton
      type="danger"
      size="mini"
      @click="showDialog = true"
      icon="el-icon-delete"
      >Delete</ElButton
    >
    <ElDialog :title="title" :visible.sync="showDialog" width="50%" center>
      <span
        >Delete {{ item.type }} "{{ item.comment }}" with value "{{
          item.value
        }}"?</span
      >
      <span slot="footer" class="dialog-footer">
        <el-button @click="showDialog = false" icon="el-icon-close"
          >Cancel</el-button
        >
        <el-button
          type="primary"
          @click="deleteItem(item.id)"
          icon="el-icon-check"
          >Confirm</el-button
        >
      </span>
    </ElDialog>
  </div>
</template>

<script>
export default {
  name: "BudgetListItem",
  components: {
    // ItemRemoveDialog,
  },
  props: {
    item: {
      type: Object,
      default: () => ({}),
    },
  },
  computed: { 
    classIcon() {
      return {
        'el-icon-top': this.item.type === 'INCOME' ? true : false,
        'el-icon-bottom': this.item.type != 'INCOME' ? true : false,
      };
    },
    classObj() {
      return {
        green: this.item.type === 'INCOME' ? true : false,
        red: this.item.type != 'INCOME' ? true : false,
      };
    },
  },
  methods: {
    deleteItem(id) {
      this.$emit("deleteItem", id);
    },
    // expenceIcon() {
    //   if (item.type === "INCOME") {
    //     return this.itemIcon = 'top';
    //   } else {
    //     return this.itemIcon = 'bottom';
    //   }
    // },
  },
  data: () => ({
    showDialog: false,
    title: "Are you shure to delete this item?",
    itemIcon: '',
  }),
};
</script>

<style scoped>
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
.green{
  color: green;
}
.red{
  color: red
}
</style>