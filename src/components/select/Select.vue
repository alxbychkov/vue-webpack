<template>
  <select
    :name="name"
    :value="modelValue"
    @change="$emit('update:modelValue', $event.target.value)"
  >
    <option value="" selected disabled>{{ caption }}</option>
    <option v-for="option in options" :value="option.value" :key="option.value">
      {{ option.title }}
    </option>
  </select>
</template>
<style lang="scss" scoped>
select {
  min-width: 250px;
  height: 30px;
  padding: 5px 10px;
  border: 1px solid #000;
  border-radius: 5px;
  font-size: 16px;
  line-height: 125%;
}
</style>
<script>
export default {
  name: "Select",
  props: {
    name: {
      type: String,
      default: null,
    },
    caption: {
      type: String,
      default: "",
    },
    value: {
      type: String,
      default: "",
    },
    modelValue: {
      type: String,
      default: null,
    },
    options: {
      type: Array,
      default: [],
    },
  },
};
</script>
