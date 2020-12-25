<template>
  <div class="backdrop">
    <form ref="form" class="form" action="" @submit.prevent="submitHandler">
      <CustomInput type="text" placeholder="Name" v-model="name" />
      <CustomInput type="text" placeholder="Surname" v-model="surname" />
      <button type="submit">Edit</button>
    </form>
  </div>
</template>

<script>
import CustomInput from "../shared/Input/Input";

export default {
  name: "edit-modal",
  props: {
    itemToEdit: {
      id: {
        type: String,
      },
      name: {
        type: String,
        default: "",
      },
      surname: {
        type: String,
        default: "",
      },
    },

    clearModal: {
      type: Function,
      default: () => null,
    },
    editItem: {
      type: Function,
      default: () => null,
    },
  },
  components: {
    CustomInput,
  },
  data() {
    return {
      id: this.itemToEdit.id,
      name: this.itemToEdit.name,
      surname: this.itemToEdit.surname,
    };
  },
  mounted() {
    this.$el.addEventListener("click", this.clickOutside);
    window.addEventListener("keypress", this.clickEscape);
  },
  beforeDestroy() {
    this.$el.removeEventListener("click", this.clickOutside);
    window.removeEventListener("keypress", this.clickEscape);
  },
  methods: {
    submitHandler() {
      if (!this.name && !this.surname) return;

      const formData = {
        name: this.name,
        surname: this.surname,
        id: this.id,
      };

      this.editItem(formData);
      this.clearModal();
    },

    clickOutside({ target }) {
      if (this.$refs.form && !this.$refs.form.contains(target)) {
        this.clearModal();
      }
    },

    clickEscape({ key }) {
      if (key === "Escape") {
        this.clearModal();
      }
    },
  },
};
</script>

<style scoped>
@import url("./ModalEdit.css");
</style>
