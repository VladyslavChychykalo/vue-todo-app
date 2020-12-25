<template>
  <div>
    <Todo @add="addItem" />
    <TodoItem
      :items="items"
      :deleteItem="deleteItem"
      :editField="editField"
      :editItem="editItem"
    />
  </div>
</template>

<script>
import Todo from "../components/Todo";
import TodoItem from "../components/TodoItem";
// import axios from "axios";

export default {
  name: "home",
  data() {
    return {
      items: [],
    };
  },
  components: {
    Todo,
    TodoItem,
  },
  mounted() {
    this.axios.get("http://localhost:3001").then((responsive) => {
      this.items = responsive.data;
    });
  },
  methods: {
    addItem(item) {
      console.log(this.items);
      console.log(item);
      this.items.unshift(item);
    },
    deleteItem(id) {
      if (!id) return;
      this.items = this.items.filter((el) => el.id !== id);
    },
    editField(id, key, value) {
      console.log(id, name, value);
      this.items = this.items.map((el) =>
        el.id === id ? { ...el, [key]: value } : el
      );
      console.log(this.items);
    },
    editItem(editedItem) {
      this.items = this.items.map((el) =>
        el.id === editedItem.id ? editedItem : el
      );
    },
  },
};
</script>
