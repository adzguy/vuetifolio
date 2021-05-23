<template>
  <b-container class="height">
    <header class="py-3">
      <NavBar />
    </header>

    <div
      class="pt-5"
      style="font-size: 26px; font-weight: 600; color: #2c3e50"
      v-if="errors"
    >
      Sorry! It seems we can't fetch data right now 😥
    </div>

    <div v-else>
      <div
        class="pt-5"
        style="font-size: 26px; font-weight: 600; color: #2c3e50"
        v-if="loading"
      >
        😴 Loading ...
      </div>
      <div v-else>
        <h2>Fetched Repository details from GitHub API</h2>
        <div class="row row-cols-1 row-cols-md-3">
          <Card
            v-for="project in projectsList"
            :key="project.id"
            :project="project"
          />
        </div>

        <div v-if="!loading">
          <div v-if="projectsList.length < projects.length" class="m-3">
            <div>
              <b-button block v-on:click="loadMore()" variant="primary">
                Load More
              </b-button>
            </div>
          </div>
          <div v-else>
            <a
              href="https://github.com/adzguy"
              target="_blank"
              rel="noopener noreferrer"
              class="pt-5"
              style="font-size: 26px; font-weight: 600; color: #2c3e50"
              >Visit My GitHub</a
            >
          </div>
        </div>

        <div>
          <h2>Development Skills</h2>
          <b-list-group horizontal="sm" class="justify-content-center p-2">
            <b-list-group-item
              pill
              class="mx-1 rounded-pill"
              style="color: rgb(55, 55, 117)"
              v-for="(skill, index) in skills"
              :key="index"
              >{{ skill }}</b-list-group-item
            >
          </b-list-group>
        </div>
      </div>
    </div>
  </b-container>
</template>

<script>
import NavBar from "./NavBar";
import Card from "./Card";

export default {
  name: "projects",
  components: { NavBar, Card },
  data() {
    return {
      data: [],
      projects: [],
      projectsList: null,
      skills: [],
      projectsCount: 5,
      perPage: 20,
      page: 1,
      loading: true,
      errors: false,
    };
  },
  methods: {
    trimedTitle: function (text) {
      let title = text.replaceAll("-", " ").replace("_", " ");
      if (title.length > 15) {
        return title.slice(0, 15) + " ...";
      }
      return title;
    },

    trimedText: function (text) {
      //console.log(text.slice(0, 100));
      if (text === null) {
        return "This project has no description yet!";
      } else if (text.length > 100) {
        return text.slice(0, 100) + " ...";
      }
      return text;
    },

    getProjects: function () {
      this.projectsList = this.projects.slice(0, this.projectsCount);
      return this.projectsList;
    },

    fetchData: function () {
      this.axios
        .get(
          `https://api.github.com/users/adzguy/repos?per_page=${this.perPage}&page=${this.page}`
        )
        .then((response) => {
          this.projects = response.data;
          this.projects.forEach((project) => {
            if (
              project.language !== null &&
              !this.skills.includes(project.language)
            ) {
              this.skills.push(project.language);
            }
          });
        })
        .catch((error) => {
          console.log(error);
          this.errors = true;
        })
        .finally(() => {
          this.loading = false;
          this.getProjects();
        });
    },

    loadMore() {
      if (this.projectsList.length <= this.projects.length) {
        this.projectsCount += 5;
        this.projectsList = this.projects.slice(0, this.projectsCount);
      }
    },
  },

  mounted() {
    setTimeout(this.fetchData, 1000);
  },
};
</script>

<style scoped>
.height {
  min-height: 96vh !important;
}

h2 {
  font-size: 36px;
  font-weight: 900;
  color: #2c3e50;
}
p {
  font-size: 22px;
  font-weight: 100;
}
</style>