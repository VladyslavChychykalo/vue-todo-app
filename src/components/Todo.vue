<template>
  <div>
    <form action="" @submit.prevent="submitHandler">
      <CustomInput type="text" placeholder="Name" v-model="name" />
      <CustomInput type="text" placeholder="Surname" v-model="surname" />
      <button type="submit">Add</button>
    </form>
  </div>
</template>

<script>
import CustomInput from "./shared/Input/Input";
import { uuid } from "vue-uuid";

export default {
  name: "todo",
  data() {
    return {
      name: "",
      surname: "",
    };
  },
  components: {
    CustomInput,
  },
  validations: {},
  methods: {
    submitHandler() {
      if (!this.name && !this.surname) return;

      const formData = {
        id: uuid.v1(),
        name: this.name,
        surname: this.surname,
      };

      this.$emit("click", formData);
      this.resetForm();
    },

    resetForm() {
      this.name = "";
      this.surname = "";
    },
  },
};
</script>

<style scoped>
@import url("./Todo.css");
</style>
