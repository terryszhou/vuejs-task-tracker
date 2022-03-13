<template>
  <AddTask
    v-if="showAddTask"
    v-on:add-task="addTask" />
  <Tasks
    v-bind:tasks="tasks"
    v-on:delete-task="deleteTask"
    v-on:toggle-reminder="toggleReminder" />
</template>

<script>
  import AddTask from "../components/AddTask.vue"
  import Tasks from "../components/Tasks.vue"

  export default {
    name: "Home",
    props: {
      showAddTask: Boolean,
    },
    components: {
      AddTask,
      Tasks,
    },
    data() {
      return {
        tasks: []
      }
    },
    methods: {
      async addTask(task) {
        const res = await fetch("api/tasks", {
          method: "POST",
          headers: {
            "Content-type": "application/json",
          },
          body: JSON.stringify(task)
        })
        const data = await res.json()
        this.tasks = [...this.tasks, data]
      },

      async deleteTask(id) {
        if (confirm("Are you sure?")) {
          const res = await fetch(`api/tasks/${id}`, {
            method: "DELETE",
          })
          res.status === 200 
            ? this.tasks = this.tasks.filter(task => task.id !== id)
            : alert("Error deleting tasks")
        }
      },

      async toggleReminder(id) {
        const taskToToggle = await this.fetchTask(id)
        const updateTask = {...taskToToggle, reminder: !taskToToggle.reminder}
        const res = await fetch(`api/tasks/${id}`, {
          method: "PUT",
          headers: {
            "Content-type": "application/json",
          },
          body: JSON.stringify(updateTask)
        })
        const data = await res.json()
        this.tasks = this.tasks.map(task => (
          task.id === id 
            ? {...task, reminder: data.reminder} 
            : task
        ))
      },

      async fetchTasks() {
        const res = await fetch("api/tasks")
        const data = await res.json()
        return data
      },

      async fetchTask(id) {
        const res = await fetch(`api/tasks/${id}`)
        const data = await res.json()
        return data
      }
    },
    async created() {
      this.tasks = await this.fetchTasks()
    }
  }
</script>
