<template>
  <div v-bind:class="[task.reminder && 'reminder', 'task']">
    <h3>
      {{ task.text }} 
      <i v-on:click="onDelete(task.id)" class="fas fa-times" />
    </h3>
    <p>{{ task.day }}</p>
  </div>
</template>

<script>
  export default {
    name: "Task",
    props: {
      task: Object,
    },
    methods: {
      onDelete(id) {
        console.log(id)
      }
    }
  }
</script>

<style scope>
  .fas {
    color: red;
  }

  .task {
    background: #f4f4f4;
    margin: 5px;
    padding: 10px 20px;
    cursor: pointer;
  }

  .task.reminder {
    border-left: 5px solid green;
  }

  .task h3 {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
</style>
