<template>
  <div v-if="haveProfile" class="git_profile">
    <img class="git_profile-avatar" :src="profile.avatar_url" alt="avatar" />
    <div>Username: {{ profile.login || "" }}</div>
    <div>Creation date: {{ profile.created_at || "" }}</div>
  </div>
  <div class="git_profile-repos" v-if="haveRepose">
    Repos:
    <div
      class="git_profile-repos-line"
      v-for="{ id, html_url, description, created_at } in profile.repos"
      :key="id"
    >
      <div>Link to the github repository: {{ html_url || "" }}</div>
      <div>Repository description: {{ description || "" }}</div>
      <div>Repository creation date: {{ created_at || "" }}</div>
    </div>
  </div>
  <div v-else></div>
</template>

<script>
export default {
  name: "GitProfile",
  props: {
    profile: { type: Object, default: () => {} },
  },
  computed: {
    haveRepose() {
      return this.profile.repos?.length > 0;
    },
    haveProfile() {
      return Object.keys(this.profile).length > 0;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.git_profile-repos-line {
  border: 1px solid black;
  border-radius: 10px;
  padding: 10px;
  margin: 10px 0;
}
.git_profile-avatar {
  width: 40px;
}
</style>
