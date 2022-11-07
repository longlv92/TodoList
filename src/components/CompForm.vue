<template>
  <!-- FORM : START -->
  <b-col cols="12" lg="6">
    <!-- ADD : START -->
    <b-col class="mb-3 add-task d-grid gap-2">
      <b-button v-if="!isShowForm" v-on:click="handleShowTask" variant="info"
        >Add Task</b-button
      >
      <b-button v-else v-on:click="handleShowTask" variant="primary"
        >Close Form</b-button
      >
    </b-col>
    <!-- ADD : END -->

    <form action="" method="POST" inline v-if="isShowForm">
      <b-row class="g-4">
        <b-col class="col-auto">
          <label class="sr-only" for="">label</label>
          <b-form-input
            type="text"
            class="form-control"
            placeholder="Task Name"
            v-model="taskName"
          />
        </b-col>
        <b-col class="col-auto">
          <label class="sr-only" for="">label</label>
          <select v-model="level" class="form-control" required="required">
            <option value="0">Small</option>
            <option value="1">Medium</option>
            <option value="2">High</option>
          </select>
        </b-col>
        <b-col class="col-auto">
          <b-button
            v-if="taskSelected === null"
            v-on:click="handleAddTask"
            variant="primary"
            >Submit</b-button
          >
          <b-button v-else v-on:click="handleEditTask" variant="primary"
            >Update</b-button
          >
        </b-col>
        <b-col class="col-auto">
          <b-button v-on:click="handleCancel">Cancel</b-button>
        </b-col>
      </b-row>
    </form>
  </b-col>
  <!-- FORM : END -->
</template>

<script>
import { v4 as uuidv4 } from "uuid";
export default {
  name: "comp-form",
  props: {
    isShowForm: { type: Boolean, default: false },
    taskSelected: { type: Object, default: null },
  },
  data() {
    return {
      taskName: "",
      level: 0,
    };
  },
  watch: {
    taskSelected: function (newData) {
      if (newData !== null) {
        this.taskName = newData.name;
        this.level = newData.level;
      }
    },
  },
  methods: {
    handleEditTask() {
      let objTaskEdit = {
        id: this.taskSelected.id,
        name: this.taskName,
        level: parseInt(this.level),
      };
      this.$emit("handleEditTaskById", objTaskEdit);
      this.handleResetData();
    },
    handleAddTask() {
      let objTask = {
        id: uuidv4(),
        name: this.taskName,
        level: parseInt(this.level),
      };
      this.$emit("handleAddNewTask", objTask);
      this.handleCancel();
    },
    handleShowTask() {
      this.$emit("toggleForm");
    },
    handleCancel() {
      this.$emit("toggleForm");
      this.handleResetData();
    },
    handleResetData() {
      this.taskName = "";
      this.level = 0;
    },
  },
};
</script>

<style scoped>
</style>