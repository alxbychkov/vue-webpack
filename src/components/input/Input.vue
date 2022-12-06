<template>
  <input
    :type="type"
    :name="name"
    :placeholder="placeholder"
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
    :required="required"
  />
</template>
<script>
export default {
  name: "Input",
  data() {
    return {};
  },
  props: {
    type: {
      type: String,
      default: "text",
    },
    name: {
      type: String,
      default: null,
    },
    placeholder: {
      type: String,
      default: null,
    },
    modelValue: {
      type: String,
      default: null,
    },
    required: {
      type: Boolean,
      default: false,
    },
  },
};
</script>
<style lang="scss" scoped>
input:not([type="checkbox"]) {
  min-width: 250px;
  height: 30px;
  padding: 5px 10px;
  border: 1px solid #000;
  border-radius: 5px;
  font-size: 16px;
  line-height: 125%;
}

input.error {
  border-color: red;
  color: red;
  outline-color: red;
}
</style>
