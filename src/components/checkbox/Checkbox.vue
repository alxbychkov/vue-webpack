<template>
  <label :for="id" class="checkbox-label">
    <input
      type="checkbox"
      :name="name"
      :id="id"
      :checked="modelValue"
      :required="required"
      @change="$emit('update:modelValue', !this.modelValue)"
    />
    {{ caption }}
  </label>
</template>
<script>
export default {
  name: "Checkbox",
  props: {
    name: {
      type: String,
      default: null,
    },
    id: {
      type: String,
      default: null,
    },
    modelValue: {
      type: Boolean,
      default: false,
    },
    caption: {
      type: String,
      default: "",
    },
    required: {
      type: Boolean,
      default: false,
    },
  },
};
</script>
<style lang="scss" scoped>
.checkbox-label {
  display: flex;
  align-items: center;
  gap: 10px;
  cursor: pointer;
  line-height: 1;

  input[type="checkbox"] {
    cursor: pointer;
    width: 15px;
    height: 15px;
    font-size: 12px;
    margin: 2px 0;
  }
}
</style>
