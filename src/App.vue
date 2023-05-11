
<template>
  
  <div id = "ToDoListApp">
      <img alt="Boise Cascade Logo" src="./assets/bc.png" style = "width: 5%" /> <!-- Image size reduced -->
      <ToDoList msg="Justin's Task List"/> <!-- App Title -->
  </div>
  
</template>


<script>

import ToDoList from './components/ToDoList.vue'

export default {
  name: 'ToDoListApp',
  components: {
    ToDoList
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #000000;
  margin-top: 10px;
}

</style>
