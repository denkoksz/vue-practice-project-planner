<template>
  <div class="home">
    <FilterNav @filterChange="currentFilter = $event" :current="currentFilter"/>
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete"/>
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from "@/components/SingleProject";
import FilterNav from "@/components/FilterNav";

export default {
  name: 'HomeView',
  data() {
    return {
      projects: [],
      currentFilter: 'all'
    }
  },
  computed: {
    filteredProjects() {
        if (this.currentFilter === 'completed') {
          return this.projects.filter(project => project.complete)
        }
        if (this.currentFilter === 'ongoing') {
          return this.projects.filter(project => !project.complete)
        }
        return this.projects
    }
  },
  components: {
    SingleProject,
    FilterNav
  },
  mounted() {
    fetch('http://localhost:3000/project')
    .then(response => response.json())
    .then(data => this.projects = data)
    .catch(error => console.log(error.message))
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((project) => {
        return project.id !== id
      })
    },
    handleComplete(id) {
      let project = this.projects.find(project => {
        return project.id ===id
      })
      project.complete = !project.complete
    }
  }
}
</script>
