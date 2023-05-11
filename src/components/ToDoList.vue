<template>

  <h1>{{ msg }}</h1> <!-- Page Title -->

  <input v-model="task" placeholder="new task" @keyup.enter="addTask"> <!-- Input Text Box -->
  
  <form @submit.prevent="addTask">
    <button type="submit" @click = "addTask" class="addButton" >Add</button> <!-- Add Task Button -->
  </form>
  
  <!-- List of Tasks -->

  <div>
    <ul class="task-list">
      <li v-for="todo in tasks" :key="todo.id" class="task-item">
        <div>
          {{ todo.text }}
        </div>
      </li>
    </ul> 
  </div>

</template>

<script>

import { ref } from "vue";

  export default {

    name: 'ToDoList',
    props: {
      msg: String
    },
    data() {

      const task = ref("");
      const tasks = ref([]);
      
      
      function addTask() {
        if (task.value) {
          tasks.value.push({
            text: task.value,
            id: Date.now(),
          });
          task.value = "";
        }
      }
      
      return {
        task,
        tasks,
        addTask,
      };
    }


    
  }

</script>



<style scoped>

  ::placeholder { /* Centers the place holder in text box */ 
    text-align: center; 
  }

  .addButton {
    padding: 6px 8px;
    /* margin-left: 150px; */
    margin-top: 4px;
    margin-bottom: 8px;

    font-size: 10px;
    background-color: rgb(1, 196, 255);
    color: rgb(255, 255, 255);
    border: none;
    border-radius: 10px;
    cursor: pointer;
  }

  .task-list {
    display: flex;
    border: 1px;
    margin-left: 400px;
    margin-right: 400px;
    flex-direction: column; /* oldest task stays on top of stack */
  }

  .task-item {
    background-color: rgba(209, 79, 133, 0.13);
    padding: 5px;
    margin-bottom: 1%;
    margin-top: 1%;
    border: 1px solid;
    border-radius: 1px;
    min-height: 10px;
    font-size: 10px;
    font-weight: bold;
  }

  h3 {
    margin: 40px 0 0;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }
  a {
    color: #1575f3;
  }
</style>
