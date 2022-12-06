<template>
  <button :disabled="disable" @click.prevent="$emit('onClick')">
    {{ caption }}
  </button>
</template>
<script>
export default {
  name: "Button",
  props: {
    caption: {
      type: String,
      default: "",
    },
    disable: {
      type: Boolean,
      default: false,
    },
  },
};
</script>
<style lang="scss" scoped>
button {
  min-width: 250px;
  height: 30px;
  padding: 5px 10px;
  border: 1px solid #000;
  border-radius: 5px;
  font-size: 16px;
  line-height: 125%;
  cursor: pointer;
}
button:disabled {
  cursor: no-drop;
}
</style>
