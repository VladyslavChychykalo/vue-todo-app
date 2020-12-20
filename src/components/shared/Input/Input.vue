<template>
  <div class="inputField">
    <label
      >Custom Text
      <input
        :type="type"
        :placeholder="placeholder"
        :value="value"
        @input="updateValue($event.target.value)"
      />
    </label>
  </div>
</template>

<script>
export default {
  name: "custom-input",
  props: {
    value: {
      type: String,
    },
    type: {
      type: String,
      default: "text",
    },
    placeholder: {
      type: String,
      default: "Text",
    },
  },
  methods: {
    updateValue(value) {
      this.$emit("input", value);
    },
  },
};
</script>