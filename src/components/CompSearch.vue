<template>
  <b-col cols="12">
    <b-col class="input-group">
      <input
        v-bind:value="strSearch"
        v-on:input="handleSearch"
        type="text"
        class="form-control"
        placeholder="Search for..."
      />
      <span class="input-group-append">
        <b-button v-on:click="handleClear" variant="info">Clear!</b-button>
      </span>
    </b-col>
  </b-col>
</template>

<script>
export default {
  name: "comp-search",
  props: {
    strSearch: { type: String, default: "" },
  },
  data() {
    return {};
  },
  methods: {
    handleClear() {
      this.$emit("handleSearch", "");
    },
    handleSearch(e) {
      this.$emit("handleSearch", e.target.value);
    },
  },
};
</script>

<style scoped>
</style>