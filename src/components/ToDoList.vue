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

    <h5 class="sortTitle">Sort by...</h5>
    
    <input type = "radio" v-model = "order" name="sort" value = "0">Oldest
    
    <input type = "radio" v-model = "order" name="sort" value = "1">Recent

  </div>

  <!-- List of Tasks -->

  <section>
    <ul class="task-list">
      <li v-for="todo in sortedTasks" :key="todo.id"  @click = "toggleCompletion(todo)" class="task-item">
          
        <div>
          {{ todo.text }}
          {{ todo.completed }} <!-- is the task completed? -->
        </div>

      </li>
    </ul> 
  </section>

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
            completed: false, /* Completed flag to remove tasks */
          });
          task.value = "";
        }
      }
    
      return {
        order:0,
        task,
        tasks,
        addTask,
      };
    },
    computed: { // Based on the Radio Sorting Buttons
      sortedTasks() {
        if (this.order === "1") {
          return this.tasks.slice().reverse();
        }
        else {
          return this.tasks;
        }
      }
    },
    methods: {
      toggleCompletion() {
        alert("test");
      }
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
    margin-bottom: 1px;

    font-size: 20px;
    background-color: rgb(1, 196, 255); /* Tile Color */
    color: rgb(255, 255, 255); /* Font Color */

    border: none;
    border-radius: 10px;
    cursor: pointer;
  }

  .sortTitle {
    margin-bottom: 5px; /* Removes the excess space between title and buttons */
  }

  .task-list {
    text-align: center;
    display: flex;
    border-width: 1px;
    margin-left: 600px;
    margin-right: 600px;
    flex-direction: column; /* oldest task stays on top of stack */
  }

  .task-item {
    text-align: center;
    padding: 12px;
    margin-bottom: 1%;
    margin-top: 1%;

    border: 1px solid;
    border-radius: 1px;
    min-height: 13px;

    font-size: 15px;
    font-weight: bold;
  }

  .task-item:hover { /* Hovering over tasks prior to completing them */
    background-color: rgba(209, 79, 133, 0.13);
    cursor: pointer;
    text-decoration: line-through;
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
