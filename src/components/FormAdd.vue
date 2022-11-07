<template>
  <b-col class="mb-3 add-task d-grid gap-2">
    <b-button v-on:click="onClickAddTask" variant="info">Add Task</b-button>
  </b-col>
</template>

<script>
export default {
  name: "form-add",
  data() {
    return {};
  },
  methods: {
    onClickAddTask() {
      this.$emit("handleAddTask");
    },
  },
};
</script>