<template>
  <div class="edit-project">
    <form @submit.prevent="handleSubmit">
      <input type="text" required placeholder="title" v-model="title">
      <textarea required placeholder="details" v-model="details"></textarea>
      <button>Edit</button>
    </form>
  </div>
</template>

<script>
export default {
  props: ['id'],
  data(){
    return {
      title: '',
      details: '',
      url: `https://syed-project-planner.herokuapp.com/projects/${this.id}`
    }
  },
  mounted(){
    fetch(this.url)
    .then(res => res.json())
    .then(data => {
      this.title = data.title
      this.details = data.details
    })
  },
  methods: {
    handleSubmit(){
      const project = {
        title: this.title,
        details: this.details
      }
      fetch(this.url, {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(project)
      })
      .then(() => this.$router.push({ name: 'Home' }))
      .catch(error => console.log(error.message))
    }
  }
}
</script>

<style>

</style>