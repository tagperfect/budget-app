<template>
  <ElCard class="form-card">
    <ElForm :model="formData" ref="addItemForm" :rules="rules">
      <ElFormItem label="Type" prop="type">
        <ElSelect
          class="type-select"
          v-model="formData.type"
          placeholder="Choose type..."
        >
          <ElOption lable="Income" value="INCOME" />
          <ElOption lable="Expense" value="EXPENSE" />
        </ElSelect>
      </ElFormItem>
      <ElFormItem label="Comment" prop="comment">
        <ElInput v-model="formData.comment" />
      </ElFormItem>
      <ElFormItem label="Value" prop="value">
        <ElInput v-model.number="formData.value" />
      </ElFormItem>
    </ElForm>
    <ElButton type="primary" @click="onSubmit">Submit</ElButton>
  </ElCard>
</template>

<script>
// const expenseType = document.querySelector('select.type-select');
export default {
  name: "FormAdd",
  data: () => ({
    formData: {
      type: "",
      comment: "",
      value: 0,
    },
    rules: {
      type: [
        { required: true, message: "Please select type", trigger: "change" },
      ],
      comment: [
        { required: true, message: "Please add comment", trigger: "blur" },
      ],
      value: [
        { required: true, message: "Please input value", trigger: "change" },
        {
          type: "number",
          message: "Value must be a Number",
          trigger: "change",
        },
        {validator: (rule, value, callback) => {
        if(value !== 0){
          callback();
        } else {
          callback('Zero is not acceptable');
        }
       }, trigger: 'blur'}
      ],
    },
    checkValue: (rule, value, callback) => {
      if (!value) {
        return callback(new Error('Please input the value'));
      }
      setTimeout(() => {
        if (!Number.isInteger(value)) {
          callback(new Error('Please input digits'));
        } else {
          if (value === 0) {
            callback(new Error('Value must be greater than 0'));
          } else {
            callback();
          }
        }
      }, 1000);
    },
  }),
  methods: {
    onSubmit() {
      if (this.formData.value === 0) return;
      this.formData.value = Math.abs(this.formData.value);
      if (this.formData.type === "EXPENSE") {
        this.formData.value *= -1;
      }
      this.$refs.addItemForm.validate((valid) => {
        if (valid) {
          this.$emit("submitForm", { ...this.formData });
          this.$refs.addItemForm.resetFields();
        }
      });
    },
  },
};
</script>

<style scoped>
.form-card {
  max-width: 500px;
  margin: auto;
}
.type-select {
  width: 100%;
}
</style>