<template>
  <el-form
    ref="innerForm"
    :model="formData"
    :rules="{}"
  >{{vModel}}
    <el-form-item
      label="First name"
      prop="firstName"
    >
      <input
        ref="inner"
        :type="type"
        v-model="formData[vModel]"
      >
    </el-form-item>
  </el-form>
</template>

<script>
  export default {
    data() {
      return {
        formData: {}
      };
    },
    props: ["type", "vModel"],
    methods: {
      validate() {
        let self = this;
        console.log("IINN", this.$refs.innerForm);
        return new Promise((resolve, reject) => {
          //   console.log("this.$refs.form::", this.$refs.form);
          console.log("valid::", true);
          this.$refs.innerForm.validate(valid => {
            console.log("st 1 this.modal::", this.formData);
            this.$emit("on-inner-validate", true, this.formData);
            resolve(valid);
          });
        });
      }
    }
  };
</script>

<style>
</style>
