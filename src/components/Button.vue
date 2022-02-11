<template>
  <button
    class="btn"
    v-bind:style="{ background: color }"
    v-on:click="onClick()" >
    {{ text }}
  </button>
</template>

<script>
  export default {
    name: "Button",
    props: {
      text: String,
      color: String,
    },
    methods: {
      onClick() {
        this.$emit("toggle-add-task")
      }
    }
  }
</script>
