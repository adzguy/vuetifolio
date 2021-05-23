<template>
  <b-container class="height">
    <b-avatar size="8em" class="animate__animated animate__pulse"></b-avatar>
    <div class="animate__animated animate__pulse">
      <h1>Vuetifolio</h1>
      <p>VueJS, VueRouter, BootstrapVue, Axios, GitHub API, and GitHub Pages</p>
    </div>
    <div class="animate__animated animate__backInUp">
      <router-link to="/projects" class="skills">Projects/Skills</router-link>
    </div>
  </b-container>
</template>

<script>
export default {
  name: "home",
};
</script>
<style scoped>
h1 {
  font-size: 36px;
  font-weight: 900;
  color: brown;
}
p {
  font-size: 22px;
  font-weight: 100;
  padding: 2rem;
}
.skills {
  text-transform: uppercase;
  text-decoration: none;
  color: rgb(55, 55, 117);
  font-size: 18px;
  font-weight: 900;
  line-height: 21px;
}
.skills:hover {
  color: brown;
}
.height {
  height: 96vh !important;
  padding: 20%;
}
</style>
