<template>
  <b-col cols="12" lg="6">
    <b-row>
      <comp-sort
        v-bind:orderBy="orderBy"
        v-bind:orderDir="orderDir"
        v-on:handleSort="handleSort"
      />
      <comp-search
        v-on:handleSearch="handleSearch"
        v-bind:strSearch="strSearch"
      />
    </b-row>
  </b-col>
</template>

<script>
import CompSort from "./CompSort";
import CompSearch from "./CompSearch";

export default {
  name: "comp-control",
  components: {
    CompSort,
    CompSearch,
  },
  props: {
    strSearch: { type: String, default: "" },
    orderBy: { type: String, default: "name" },
    orderDir: { type: String, default: "asc" },
  },
  data() {
    return {};
  },
  methods: {
    handleSearch(data) {
      this.$emit("handleSearch", data);
    },
    handleSort(data) {
      this.$emit("handleSort", data);
    },
  },
};
</script>

<style scoped>
</style>