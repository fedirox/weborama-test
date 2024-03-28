<template>
  <div class="search_form">
    <input
      v-model="searchValue"
      class="search_form-input"
      placeholder="Search for your repo"
    />
    <button class="search_form-button" @click="handleValidation">
      Validate
    </button>
  </div>
</template>

<script>
export default {
  name: "SearchForm",
  data() {
    return {
      searchValue: "",
    };
  },
  methods: {
    async handleValidation() {
      this.$emit("handle-validate", this.searchValue);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.search_form {
  margin-bottom: 10px;
}
.search_form-input {
}
.search_form-button {
}
</style>
