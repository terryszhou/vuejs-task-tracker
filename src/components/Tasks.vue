<template>
  <div v-for="task in tasks" v-bind:key="task.id">
    <Task v-bind:task="task"/>
  </div>
</template>

<script>
  import Task from "./Task.vue"

  export default {
    name: "Tasks",
    props: {
      tasks: Array,
    },
    components: {
      Task,
    },
  }
</script>
