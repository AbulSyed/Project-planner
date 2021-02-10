<template>
  <div class="filter-nav">
    <button @click="handleClick('all')" :class="{ active: status === 'all' }">All</button>
    <button @click="handleClick('completed')" :class="{ active: status === 'completed' }">Completed</button>
    <button @click="handleClick('ongoing')" :class="{ active: status === 'ongoing' }">Ongoing</button>
  </div>
</template>

<script>
export default {
  props: ['status'],
  methods: {
    handleClick(by){
      this.$emit('filterBy', by)
    }
  }
}
</script>

<style>
  .filter-nav button {
    background: none;
    border: none;
    color: #bbb;
    outline: none;
    font-size: 12px;
    text-transform: uppercase;
    margin-right: 10px;
    letter-spacing: 1px;
    font-weight: bold;
    cursor: pointer;
  }
  .filter-nav button.active {
    color: #555;
  }
</style>