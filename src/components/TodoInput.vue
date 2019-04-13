<script>
export default {
  name: "TodoInput",
  data() {
    return {};
  },
  methods: {
    onInputText() {},
    onSubmit() {
      let text = { text: this.inputText };
      this.$emit("add-todo", text);
    }
  }
};
</script>

<template></template>

<style>
</style>


