<template>
  <div class="add-project">
    <form @submit.prevent="handleSubmit">
      <input type="text" required placeholder="title" v-model="title">
      <textarea required placeholder="details" v-model="details"></textarea>
      <button>Add</button>
    </form>
  </div>
</template>

<script>
export default {
  data(){
    return {
      title: '',
      details: ''
    }
  },
  methods: {
    handleSubmit(){
      const project = {
        title: this.title,
        details: this.details,
        complete: false
      }
      fetch('https://syed-project-planner.herokuapp.com/projects', {
        method: 'POST',
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
  form {
    background: white;
    padding: 20px;
    border-radius: 10px;
  }
  input {
    padding: 10px;
    border: 1px solid #ddd;
    width: 100%;
    box-sizing: border-box;
    margin-bottom: 10px;
    outline: none;
  }
  textarea {
    border: 1px solid #ddd;
    padding: 10px;
    width: 100%;
    box-sizing: border-box;
    height: 100px;
    outline: none;
  }
  form button {
    display: block;
    margin: 20px auto 0;
    background: #00ce89;
    color: white;
    padding: 10px;
    border: 0;
    border-radius: 6px;
    font-size: 16px;
  }
</style>