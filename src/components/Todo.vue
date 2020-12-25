<template>
  <div>
    <form action="" @submit.prevent="submitHandler()">
      <CustomInput type="text" placeholder="Name" v-model="name" />
      <CustomInput type="text" placeholder="Surname" v-model="surname" />
      <button type="submit">Add</button>
    </form>
  </div>
</template>

<script>
import CustomInput from "./shared/Input/Input";
import { uuid } from "vue-uuid";
import axios from "axios";

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
    addItem(value) {
      console.log(value);
      this.$emit("add", value);
    },
    submitHandler() {
      if (!this.name && !this.surname) return;

      const formData = {
        name: this.name,
        surname: this.surname,
      };

      axios
        .post("http://localhost:3001", formData)
        .then((response) => {
          this.addItem(response.data);
        })
        .catch((error) => {
          console.log(error);
        });

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
