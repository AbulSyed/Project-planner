<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <single-project :project="project" @delete="handleDelete" @complete="handleComplete"></single-project>
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from '../components/SingleProject.vue'

export default {
  components: { SingleProject },
  data(){
    return {
      projects: []
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
    handleComplete(id){
      const project = this.projects.find(project => project.id === id)
      project.complete = !project.complete
    }
  }
}
</script>

<style>

</style>