<template>
  <Users />
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Users from './components/Users.vue'

export default defineComponent({
  name: 'App',
  components: {
    Users
  }
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  line-height: 1.415;
}
body {
  margin: 0;
}
</style>
