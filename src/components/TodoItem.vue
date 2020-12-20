<template>
  <div>
    <div v-for="{ id, name, surname } of items" :key="id">
      <div>
        <p
          ref="name"
          contenteditable="true"
          @blur="editField(id, 'name', $event.target.textContent)"
        >
          {{ name }}
        </p>
      </div>

      <p
        ref="surname"
        contenteditable="true"
        @blur="editField(id, 'surname', $event.target.textContent)"
      >
        {{ surname }}
      </p>
      <button @click="deleteItem(id)">
        Delete
      </button>
      <button @click="openEditModal({ id, name, surname })">Edit2</button>
    </div>

    <ModalEdit
      :itemToEdit="itemToEdit"
      v-if="itemToEdit"
      :editItem="editItem"
      :clearModal="clearModal"
    />
  </div>
</template>

<script>
import ModalEdit from "../components/ModalEdit/ModalEdit";

export default {
  data() {
    return {
      itemToEdit: null,
    };
  },
  props: {
    items: {
      type: Array,
      default: [],
    },
    deleteItem: {
      type: Function,
      default: () => null,
    },
    editField: {
      type: Function,
      default: () => null,
    },
    editItem: {
      type: Function,
      default: () => null,
    },
  },
  components: {
    ModalEdit,
  },
  methods: {
    openEditModal(item) {
      this.itemToEdit = item;
    },

    clearModal() {
      this.itemToEdit = null;
    },
  },
};
</script>
