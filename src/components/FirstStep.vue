<template>
  <el-form
    :model="model"
    :rules="rules"
    ref="form"
  >{{formData}}
    <template v-for="(formItem,itemIndex) in formItemList">
      <el-form-item
        label="First name"
        prop="firstName"
        :key="itemIndex"
      >
        <component
          :is="formItem.name"
          :type="formItem.type"
          :vModel="formItem.vModel"
          :ref="formItem.refName"
          @on-inner-validate="onInnerValidate"
        ></component>
        <!-- <el-input
          v-model="model.firstName"
          placeholder="First name"
        ></el-input> -->
      </el-form-item>
    </template>
    <!--    <el-form-item
      label="Last Name"
      prop="lastName"
    >
      <el-input
        v-model="model.lastName"
        placeholder="Last name"
      ></el-input>
    </el-form-item>
    <el-form-item
      label="Email"
      prop="email"
    >
      <el-input
        v-model="model.email"
        placeholder="Email"
      ></el-input>
    </el-form-item> -->
  </el-form>
</template>

<script>
  import DInput from "../dViews/DInput";
  export default {
    components: { DInput },
    props: ["formItemList"],
    data() {
      return {
        formData: {},
        model: {
          firstName: "",
          lastName: "",
          email: ""
        },
        rules: {
          /*      firstName: [
                                {
                                required: true,
                                  message: "First name is required",
                                  trigger: "blur"
                                }
                              ],
                              lastName: [
                                {
                                  required: true,
                                  message: "Last name is required",
                                  trigger: "blur"
                                }
                              ],
                              email: [
                                {
                                  required: true,
                                  message: "Email is required",
                                  trigger: "blur"
                                },
                                {
                                  type: "email",
                                  message: "Invalid email",
                                  trigger: "change"
                                }
                              ]
                              */
        }
      };
    },
    methods: {
      setFromParent(data) {
        console.log("Seeting from parent data::", data);
      },
      onInnerValidate(valid, formData) {
        this.formData = { ...formData };
        console.log("ON INNER Valdite", formData, this.$refs.form.validate());
        return new Promise((resolve, reject) => {
          // console.log("this.$refs.form::", this.$refs.form);
          this.$refs.form.validate(valid => {
            console.log("validIN::", valid);
            // console.log("st 1 this.modal::", this.model);
            this.$emit("on-validate", valid, this.formData);
            resolve(valid);
          });
        });
      },

      validate() {
        console.log("IN1", this.$refs.form);
        for (let item of this.formItemList) {
          console.log(item);
          return this.$refs[item.refName][0].validate();
        }
        // return this.$refs[ref][0].validate();
        /*  return new Promise((resolve, reject) => {
                                                            // console.log("this.$refs.form::", this.$refs.form);
                                                            this.$refs.form.validate(valid => {
                                                              // console.log("valid::", valid);
                                                              // console.log("st 1 this.modal::", this.model);
                                                              this.$emit("on-validate", valid, this.model);
                                                              resolve(valid);
                                                            });
                                                          }); */
      }
    }
  };
</script>

<style>
</style>
