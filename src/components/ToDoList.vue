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

  <div v-if="tasks.length > 1">

    <h5 class="sortTitle">Sort by...</h5>
    
    <input type = "radio" v-model = "order" name="sort" value = "0">Oldest    
    <input type = "radio" v-model = "order" name="sort" value = "1">Recent

  </div>

  <!-- Active Tasks -->

  <h3 v-bind:title='showActive' v-if="tasks.length > 0" @click="toggleActiveDropdown" class="taskHeader">
    Active Tasks <i :class="{'fa-chevron-down': !showActiveTasks, 'fa-chevron-up': showActiveTasks}" class="fas"></i>
  </h3>


  <section>
    <ul class="task-list" v-if="showActiveTasks">
      <li v-bind:title='completeMessage' v-for="(todo, index) in sortedTasks" :key="todo.id"  @click = "remTask(todo, index)" class="task-item">
      
        <div>
          {{ todo.text }}
        </div>

      </li>
    </ul> 
  </section>

  
  <!-- Completed Tasks -->

  <h3 v-bind:title='showCompleted' v-if="completedTasks.length > 0" @click="toggleCompletedDropdown" class="taskHeader">
   Completed Tasks <i :class="{'fa-chevron-down': !showCompletedTasks, 'fa-chevron-up': showCompletedTasks}" class="fas"></i>
  </h3>


  <section>
    <ul class="task-list" v-if="showCompletedTasks">
      <li v-bind:title='restoreMessage' v-for="(todo, index) in completedTasks" :key="todo.id" @click = "restoreTask(todo,index)" class="completed-items">
       
        <div>
          {{ todo.text }}
        </div>

      </li>
    </ul> 
  </section>

</template>



<script>

import { ref } from "vue";

  export default {

    name: 'ToDoList',
    upHere: false,
    props: {
      msg: String
    },
    data() {

      const task = ref(""); //define const vars
      const tasks = ref([]);
      const completedTasks = ref([]);
      const completeMessage = "Mark Completed";
      const showActive = "Toggle Active Tasks";
      const showCompleted = "Toggle Completed Tasks";
      const restoreMessage = "Restore Task";
      
      function addTask() {
        if (task.value) {
          tasks.value.push({
            text: task.value,
            id: Date.now(),
          });
          task.value = "";
        }
      }

      function remTask(elemnt, indx) {
        this.tasks.splice(indx,1);
        completedTasks.value.push(elemnt);
      }

      function restoreTask (elemnt, indx) {
        this.completedTasks.splice(indx,1);
        tasks.value.push(elemnt);
      }


      return {
        order:0,
        task,
        tasks,
        completedTasks,
        showCompletedTasks: false,
        showActiveTasks: true,
        showActive,
        showCompleted,
        completeMessage,
        restoreMessage,
        addTask,
        remTask,
        restoreTask,
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
      toggleCompletedDropdown() {
        this.showCompletedTasks = !this.showCompletedTasks;
      },
      toggleActiveDropdown() {
        this.showActiveTasks = !this.showActiveTasks;
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

    padding-left: min(30%);
    padding-right: min(30%);
    
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

  .completed-items{
    text-align: center;
    padding: 12px;
    margin-bottom: 1%;
    margin-top: 1%;

    border: 1px solid;
    border-radius: 1px;
    min-height: 13px;

    background-color: rgba(209, 79, 133, 0.13);
    text-decoration: line-through;
  }

  .completed-items:hover {
    cursor: pointer;
    text-decoration: none;
  }

  .taskHeader {
    border-bottom: 2px solid;
    border-color: aqua;
    text-align: center;

    margin-left: 43%;
    margin-right: 43%;

    cursor: pointer;
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