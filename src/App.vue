<template>
  <b-col id="app">
    <b-container>
      <comp-title />
      <b-row>
        <comp-control
          v-bind:orderBy="orderBy"
          v-bind:orderDir="orderDir"
          v-bind:strSearch="strSearch"
          v-on:handleSort="handleSort"
          v-on:handleSearch="handleSearch"
        />
        <comp-form
          v-bind:isShowForm="isShowForm"
          v-bind:taskSelected="taskSelected"
          v-on:toggleForm="toggleForm"
          v-on:handleAddNewTask="handleAddNewTask"
          v-on:handleEditTaskById="handleEditTaskById"
        />
      </b-row>
      <todo-list
        v-bind:listTask="listTaskSort"
        v-on:handleDelete="handleDelete"
        v-on:handleEdit="handleEdit"
      />
    </b-container>
  </b-col>
</template>

<script>
import TodoList from "./components/TodoList";
import CompTitle from "./components/CompTitle";
import CompControl from "./components/CompControl";
import CompForm from "./components/CompForm";

export default {
  name: "App",
  components: {
    TodoList,
    CompTitle,
    CompControl,
    CompForm,
  },
  data() {
    return {
      listTask: null,
      isShowForm: false,
      strSearch: "",
      orderBy: "name",
      orderDir: "asc",
      taskSelected: null,
    };
  },
  watch: {
    listTask: function (newTask) {
      var taskString = JSON.stringify(newTask);
      localStorage.setItem("tasks", taskString);
    },
  },
  computed: {
    listTaskSearch() {
      const { strSearch } = this;
      var newItem = this.listTask.filter((item) => {
        return item.name.toLowerCase().includes(strSearch.toLowerCase());
      });
      return newItem;
    },
    listTaskSort() {
      var listTask = [...this.listTaskSearch];
      listTask.sort(this.compareSort);
      return listTask;
    },
  },
  created() {
    let tasks = localStorage.getItem("tasks");
    if (tasks != null) {
      this.listTask = JSON.parse(tasks);
    } else {
      this.listTask = [];
    }
  },
  methods: {
    handleEditTaskById(taskEdit) {
      let index = this.listTask.findIndex((item) => item.id === taskEdit.id);
      if (index !== -1) {
        this.listTask.splice(index, 1, taskEdit);
        this.toggleForm();
      }
    },
    handleAddNewTask(newTask) {
      this.listTask.push(newTask);
    },
    handleEdit(taskEdit) {
      this.isShowForm = true;
      this.taskSelected = taskEdit;
    },
    handleDelete(taskDelete) {
      let newItems = this.listTask.filter((item) => item.id !== taskDelete.id);
      this.listTask = newItems;
    },
    compareSort(a, b) {
      var numberSort = this.orderDir === "asc" ? -1 : 1;
      // a b c d
      if (a[this.orderBy] < b[this.orderBy]) return numberSort;
      // d c b a
      else if (a[this.orderBy] > b[this.orderBy]) return numberSort * -1;
      return 0;
    },
    handleSort(data) {
      this.orderBy = data.orderBy;
      this.orderDir = data.orderDir;
    },
    handleSearch(data) {
      this.strSearch = data;
    },
    toggleForm() {
      if (this.isShowForm) this.taskSelected = null;
      this.isShowForm = !this.isShowForm;
    },
  },
};
</script>

<style>
body {
  padding: 100px 0;
}
.table > tbody > tr > td,
.table > tbody > tr > th,
.table > tfoot > tr > td,
.table > tfoot > tr > th,
.table > thead > tr > td,
.table > thead > tr > th {
  vertical-align: middle;
}

.container > .row {
  margin-top: 20px;
  margin-bottom: 30px;
}

span.badge-medium {
  padding: 11px 10px;
  margin: 0px 8px;
  font-size: 16px;
  display: inline-block;
  vertical-align: top;
}

.input-group-append .btn-info {
  border-radius: 0 0.375rem 0.375rem 0;
}

@media (max-width: 992px) {
  .add-task {
    margin-top: 50px;
  }
}
.sr-only {
  display: none;
}

.form-inline .col-auto.btn {
  margin-top: 0px !important;
}
</style>
