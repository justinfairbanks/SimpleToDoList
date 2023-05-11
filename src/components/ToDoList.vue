<template>

  <!-- Page Title -->

  <h1>{{ msg }}</h1> 

  <!-- Input Text Box -->

  <input v-model="task" placeholder="new task" @keyup.enter="addTask" class = "centered-input">
  
  <!-- Add Task Button -->
  
  <form @submit.prevent="addTask">
    <button type="submit" @click = "addTask" class="addButton" >Add</button> 
  </form>
  
  <!-- Sort Task Radio Button -->

  <div>

    <h5> Sort by...</h5>
    <input type = "radio" v-model = "color" value = "0">Newest First
    <input type = "radio" v-model = "color" value = "1">Oldest First

  </div>

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

      const task = ref(""); //define const vars
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

  ::placeholder { /* Centers the placeholder text */ 
    text-align: center; 
  }

  .centered-input {
    text-align: center; /* Makes user typing in middle of text box */
    font-size: 20px;
    padding: 4px 16px;
  }

  .addButton {
    padding: 6px 12px; /* Size of button */
    margin-left: 225px;
    margin-top: 4px;
    margin-bottom: 20px;

    font-size: 20px;
    background-color: rgb(1, 196, 255);
    color: rgb(255, 255, 255);
    border: none;
    border-radius: 10px;
    cursor: pointer;
  }

  .task-list {
    display: flex;
    border-width: 1px;
    margin-left: 600px;
    margin-right: 600px;
    flex-direction: column; /* oldest task stays on top of stack */
  }

  .task-item {
    background-color: rgba(209, 79, 133, 0.13);
    padding: 12px;
    margin-bottom: 1%;
    margin-top: 1%;
    border: 1px solid;
    border-radius: 1px;
    min-height: 13px;
    font-size: 15px;
    font-weight: bold;
  }


  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }

</style>
