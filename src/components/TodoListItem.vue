<template>
  <tr>
    <td class="text-center">{{ index }}</td>
    <td>{{ task.name }}</td>
    <td class="text-center">
      <span class="badge" v-bind:class="className">{{ getLevelName }}</span>
    </td>
    <td>
      <b-button v-on:click="handleEdit" variant="warning">Edit</b-button>
      <b-button v-on:click="handleDelete" variant="danger">Delete</b-button>
    </td>
  </tr>
</template>

<script>
import mapLevel from "../mocks/taskLevel";
export default {
  name: "todo-list-item",
  props: {
    task: { type: Object, default: null },
    index: Number,
  },
  computed: {
    getLevelName() {
      return this.mapLevel[this.task.level].name;
    },
    className() {
      return this.mapLevel[this.task.level].class;
    },
  },
  data() {
    return {
      mapLevel: mapLevel,
    };
  },
  methods: {
    handleEdit() {
      this.$emit("handleEdit", this.task);
    },
    handleDelete() {
      if (confirm("Bạn có muốn xóa task không?")) {
        this.$emit("handleDelete", this.task);
      }
    },
  },
};
</script>