<template>
  <b-col cols="12">
    <b-col class="mb-3">
      <b-dropdown id="dropdown-1" text="Sort by">
        <b-dropdown-item v-on:click="handleSort('name', 'asc')"
          >Name ASC</b-dropdown-item
        >
        <b-dropdown-item v-on:click="handleSort('name', 'desc')"
          >Name DESC</b-dropdown-item
        >
        <b-dropdown-divider />
        <b-dropdown-item v-on:click="handleSort('level', 'asc')"
          >Level ASC</b-dropdown-item
        >
        <b-dropdown-item v-on:click="handleSort('level', 'desc')"
          >Level DESC</b-dropdown-item
        >
      </b-dropdown>
      <span class="order badge bg-success badge-medium"
        >{{ orderBy }} - {{ orderDir }}</span
      >
    </b-col>
  </b-col>
</template>

<script>
export default {
  name: "comp-sort",
  props: {
    orderBy: { type: String, default: "name" },
    orderDir: { type: String, default: "asc" },
  },
  data() {
    return {};
  },
  methods: {
    handleSort(orderBy, orderDir) {
      let data = { orderBy, orderDir };
      this.$emit("handleSort", data);
    },
  },
};
</script>

<style scoped>
.order {
  text-transform: uppercase;
}
</style>