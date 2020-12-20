<template>
  <div>
    <Todo @click="addItem($event)" />
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
  methods: {
    addItem(item) {
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
