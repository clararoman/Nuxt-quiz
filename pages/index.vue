<template>
  <div class="home-wrapper">
    <div v-if="underConstruction" class="under-construction">
      <h1>Under Construction</h1>
    </div>
    <!-- <ProjectFilter :projects="projects" @clicked="getFilteredProjects" /> -->
    <div class="row" v-else>
      <div class="col-6" v-for="project in projectList" :key="project.id">
        <div class="project" v-if="project.Title!=='Snake'">
          <nuxt-link :to="project.path">
            <div class="project-background">
              <h3>{{project.Title}}</h3>
            </div>
            <div class="info">
              <p>{{project.Description}}</p>
            </div>
          </nuxt-link>
        </div>
        <div class="project" v-else-if="project.Title=='Snake'">
          <a
            target="_blank"
            href="https://codepen.io/clararoman/pen/ZZdBdR"
            v-if="project.Title=='Snake'"
          >
            <div class="project-background">
              <h3>{{project.Title}}</h3>
            </div>
            <div class="info">
              <p>{{project.Description}}</p>
            </div>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import ProjectFilter from "@/components/ProjectFilter.vue";
// import projects from "@/assets/projects/projectArray.json";
// import image from "@/assets/IMG_3357.jpg";

export default {
  data() {
    return {
      // projectList: projects,
      // profilePic: image,
      underConstruction: true
    };
  },
  components: {
    // ProjectFilter
  },
  computed: {
    projects() {
      // return;
    }
  },
  mounted() {
    // this.$store.dispatch("projects/getProjects");
  }
  // updated() {
  //   if (this.filteredProjects == null || this.filteredProjects.length < 1) {
  //     this.filteredProjects = this.projects;
  //   }
  // },
  // methods: {
  //   getFilteredProjects(filteredProjects) {
  //     this.filteredProjects = filteredProjects;
  //   }
  // }
};
</script>

<style lang="scss" scoped>
.home-wrapper {
  margin: 2rem;
  .under-construction {
    h1 {
      text-align: center;
    }
  }
  &.container {
    margin-top: 4em;
  }
  a {
    text-decoration: none;
    color: #262626;
  }
  .presentation {
    margin-bottom: 2em;
    padding: 2rem;
    background-color: #262626;
    position: relative;
    top: -2rem;
    left: -2rem;
    color: #e8e8e8;
    .img-wrapper {
      // background-image: url("../assets/IMG_3357.jpg");
      height: 200px;
      width: 200px;
      background-size: cover;
      margin: 2rem auto;
    }
    h2 {
      text-align: center;
    }
  }
  .project {
    .project-background {
      display: flex;
      align-items: center;
      height: 10em;
      background-color: $primary-color;
      margin: 1rem 0;
      color: $light;
      h3 {
        margin: 0 auto;
      }
    }
    .info {
      background-color: white;
    }
  }
}
</style>
