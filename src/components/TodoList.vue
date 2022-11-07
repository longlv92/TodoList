<template>
  <div class="card panel-success">
    <div class="card-header">List Task</div>
    <table class="table table-hover">
      <thead>
        <tr>
          <th style="width: 10%" class="text-center">#</th>
          <th>Task</th>
          <th style="width: 20%" class="text-center">Level</th>
          <th style="width: 160px">Action</th>
        </tr>
      </thead>

      <tbody v-if="listTask.length != ''">
        <todo-list-item
          v-for="(task, index) in listTask"
          v-bind:key="task.id"
          v-bind:task="task"
          v-bind:index="index + 1"
          v-on:handleDelete="handleDelete"
          v-on:handleEdit="handleEdit"
        />
      </tbody>
      <tbody v-else>
        <tr>
          <td colspan="4"><h3>List empty</h3></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import TodoListItem from "./TodoListItem.vue";

export default {
  name: "todo-list",
  components: {
    TodoListItem,
  },
  props: {
    listTask: { type: Array, default: () => [] },
  },
  data() {
    return {};
  },
  methods: {
    handleEdit(taskEdit) {
      this.$emit("handleEdit", taskEdit);
    },
    handleDelete(taskDelete) {
      this.$emit("handleDelete", taskDelete);
    },
  },
};
</script>