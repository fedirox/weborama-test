<template>
  <SearchForm @handle-validate="handleValidate" />
  <div v-if="errorMessage">{{ errorMessage }}</div>
  <GitProfile :profile="profile" />
</template>

<script>
import GitProfile from "./components/GitProfile.vue";
import SearchForm from "./components/SearchForm.vue";

export default {
  name: "App",
  data() {
    return { profile: {}, errorMessage: "" };
  },

  components: {
    GitProfile,
    SearchForm,
  },

  methods: {
    async handleFetch(value) {
      this.profile = {};
      this.errorMessage = "";
      const url = `https://api.github.com/users/${value}`;

      try {
        const profileResponse = await fetch(url);
        if (!profileResponse.ok) throw new Error("can't fetch data from url");

        const { repos_url, ...rest } = await profileResponse.json();
        this.profile = rest;

        if (!repos_url) throw new Error("can't can't find repo url");

        const reposResponse = await fetch(repos_url);
        if (!reposResponse.ok)
          throw new Error("can't fetch repos from repos_url");

        const repos = await reposResponse.json();

        this.profile = { ...this.profile, repos };
      } catch (error) {
        this.errorMessage = error?.message || "unhandled error";
      }
    },
    async handleValidate(value) {
      await this.handleFetch(value);
      console.log({ profile: this.profile.login });
    },
  },
};
</script>

<style></style>
