<template>
  <div id="app">
    <!-- <TodoList/> -->
    <Animation />
  </div>
</template>

<script>
import TodoList from './views/TodoList'
import Animation from './views/Animation'

export default {
  name: 'App',
  components: {
    TodoList,
    Animation
  }
}
</script>

<style>
</style>
