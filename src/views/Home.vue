<template>
  <div class="home">
    <filter-nav @filterBy="status = $event" :status="status"></filter-nav>
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project._id">
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
    fetch('https://syed-project-planner.herokuapp.com/projects')
    .then(res => res.json())
    .then(data => {
      this.projects = data
      console.log(data)
    })
    .catch(error => console.log(error))
  },
  methods: {
    handleDelete(id){
      this.projects = this.projects.filter(project => project._id !== id)
    },
    handleDone(id){
      const project = this.projects.find(project => project._id === id)
      project.complete = !project.complete
    }
  },
  computed: {
    filteredProjects(){
      if(this.status === 'completed'){
        return this.projects.filter(project => project.complete)
      }
      if(this.status === 'ongoing'){
        return this.projects.filter(project => !project.complete)
      }
      return this.projects
    }
  }
}
</script>

<style>

</style>