<template>
  <div>
    <NavBar />

    <main class="container">
      <div class="error" v-if="errors">
        Sorry! It seems we can't fetch data right now 😥
      </div>

      <section id="portfolio" v-else>
        <div class="loading" v-if="loading">😴 Loading ...</div>
        <div class="projects" v-else>
          <div
            v-for="project in projectsList"
            :key="project.id"
            class="card__custom"
          >
            <div class="card__custom__text">
              <div>
                <h3>{{ project.name }}</h3>
                <p>{{ project.description }}</p>
              </div>

              <div class="meta__data d_flex">
                <div class="date">
                  <h5>Updated at</h5>
                  <div>{{ new Date(project.updated_at).toDateString() }}</div>
                </div>
                <b-avatar :src="project.owner.avatar_url" size="6em"></b-avatar>
              </div>
            </div>
            <div class="card__custom__img"></div>
            <div class="card_custom__button">
              <a :href="project.html_url" target="_blank"> Code </a>
            </div>
          </div>

          <div style="text-align: center; width: 100%" v-if="!loading">
            <div v-if="projectsList.length < projects.length">
              <button class="btn_load_more" v-on:click="loadMore()">
                Load More
              </button>
            </div>
            <div v-else>
              <a href="" target="_blank" rel="noopener noreferrer"
                >Visit My GitHub</a
              >
            </div>
          </div>

          <div id="">
            <h2>Development Skills</h2>
            <ul class="">
              <li v-for="(skill, index) in skills" :key="index">{{ skill }}</li>
            </ul>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
import NavBar from "./NavBar";

export default {
  name: "projects",
  components: { NavBar },
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
          `https://api.github.com/users/fbhood/repos?per_page=${this.perPage}&page=${this.page}`
        )
        .then((response) => {
          this.projects = response.data;
          console.log(this.projects);
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