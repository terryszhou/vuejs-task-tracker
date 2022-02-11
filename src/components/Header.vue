<template>
  <header>
    <h1>{{ title }}</h1>
    <Button
      v-bind:color="showAddTask ? 'red' : 'green'"
      v-bind:text="showAddTask ? 'Close' : 'Add Task'"
      v-on:btn-click="$emit('toggle-add-task')" 
      v-show="homePage" />
  </header>
</template>

<script>
  import Button from "./Button"

  export default {
    name: "Header",
    props: {
      title: String,
      showAddTask: Boolean,
    },
    components: {
      Button,
    },
    computed: {
      homePage() {
        if (this.$route.path === "/") {
          return true
        } else {
          return false
        }
      }
    }
  }
</script>

<style scoped>
  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
  }
</style>
