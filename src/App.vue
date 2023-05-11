
<template>
  
  <img alt="Boise Cascade Logo" src="./assets/bc.png" class = "image-resize" /> <!-- This needs to be resized smaller! -->
  <!--                          Use "./assets/bc.png" for Boise Cascade Logo -->

  <ToDoList msg="Justin's To Do List"/> <!-- App Title -->

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
.image-resize
{
  width: 5%;
}

</style>
