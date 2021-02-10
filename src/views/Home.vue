<template>
  <div class="home">
    <filter-nav @filterBy="status = $event" :status="status"></filter-nav>
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <single-project :project="project" @delete="handleDelete" @done="handleDone"></single-project>
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from '../components/SingleProject.vue'
import FilterNav from '../components/FilterNav.vue'

export default {
  components: { SingleProject, FilterNav },
  data(){
    return {
      projects: [],
      status: 'all'
    }
  },
  mounted(){
    fetch('http://localhost:3000/projects')
    .then(res => res.json())
    .then(data => this.projects = data)
    .catch(error => console.log(error))
  },
  methods: {
    handleDelete(id){
      this.projects = this.projects.filter(project => project.id !== id)
    },
    handleDone(id){
      const project = this.projects.find(project => project.id === id)
      project.complete = !project.complete
    }
  }
}
</script>

<style>

</style>