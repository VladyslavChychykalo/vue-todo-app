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
      this.axios
        .post("http://localhost:3001", item)
        .then((response) => {
          this.items.unshift(response.data);
        })
        .catch((error) => {
          console.log(error);
        });

      // this.items.unshift(item);
    },
    deleteItem(id) {
      if (!id) return;
      this.axios
        .get(`http://localhost:3001/user/${id}`)
        .then((responsive) => {
          this.items = this.items.filter((el) => el.id !== responsive.data.id);
        })
        .catch((error) => {
          console.log(error);
        });

      // this.items = this.items.filter((el) => el.id !== id);
    },
    editField(id, key, value) {
      // console.log(id, name, value);
      this.items = this.items.map((el) =>
        el.id === id ? { ...el, [key]: value } : el
      );
      // console.log(this.items);
    },
    editItem(editedItem) {
      console.log(editedItem);
      this.axios
        .put(`http://localhost:3001/user/${editedItem.id}`, editedItem)
        .then((response) => {
          console.log(response.data);

          this.items = this.items.map((el) =>
            el.id === response.data.id ? response.data : el
          );
        })
        .catch((error) => {
          console.log(error);
        });
      // // =============
      // this.items = this.items.map((el) =>
      //   el.id === editedItem.id ? editedItem : el
      // );
    },
  },
};
</script>
