<template>
<div class='bg-blue-100 m-auto w-auto h-auto xl:w-6/12 h-50vh '>
<h1 class='text-3xl font-bold pb-4 pt-4'>Todo App</h1>
<todo-input class='m-5'> </todo-input>
</div>
</template>


<script>
import TodoInput from '@/components/TodoInput.vue'

export default {
  name: 'App',
  components: {
    TodoInput
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
