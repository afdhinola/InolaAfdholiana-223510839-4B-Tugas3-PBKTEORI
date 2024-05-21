<template>
    <div>
      <main id="content">
        <div v-if="activeTab === 'todos'">
          <h2>Todos</h2>
          <div class="todo-component">
            <div class="container todo-container">
              <h1 style="text-align: center;">To do List Inola 𖹭</h1>
              <div style="display: flex;">
                <input type="text" v-model="newTask" placeholder="Add new list...">
                <button @click="addTask">Add</button>
              </div>
  
              <div v-for="(task, index) in incompleteTasks" :key="index" class="task" :class="{ 'completed': task.completed }">
                <input type="checkbox" v-model="task.completed" class="checkbox">
                <div v-if="!task.editing" class="task-text">{{ task.title }}</div>
                <div v-else class="edit-mode">
                  <input v-model="task.title" class="edit-input">
                  <div class="button-group">
                    <button class="update-btn" @click="updateTask(index)">Update</button>
                    <button class="cancel-btn" @click="cancelTask(index)">Cancel</button>
                  </div>
                </div>
                <div v-if="!task.editing" class="button-group">
                  <button class="edit-btn" @click="editTask(index)">Edit</button>
                  <button class="delete-btn" @click="deleteTask(index)">Delete</button>
                </div>
              </div>
  
              <button class="filter-btn" @click="showIncomplete = !showIncomplete">
                {{ showIncomplete ? 'Show All List' : 'Show Incomplete List Only' }}
              </button>
            </div>
          </div>
        </div>
      </main>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        activeTab: 'todos',
        tasks: [],
        newTask: '',
        showIncomplete: true,
        users: [],
        selectedUser: null,
        userPosts: []
      };
    },
    computed: {
      incompleteTasks() {
        if (this.showIncomplete) {
          return this.tasks.filter(task => !task.completed);
        } else {
          return this.tasks;
        }
      }
    },
    methods: {
      addTask() {
        if (this.newTask.trim() !== '') {
          this.tasks.push({ title: this.newTask, completed: false });
          this.newTask = '';
        }
      },
      cancelTask(index) {
        this.tasks[index].editing = false;
      },
      editTask(index) {
        this.tasks[index].editing = true;
      },
      updateTask(index) {
        this.tasks[index].editing = false;
      },
      deleteTask(index) {
        this.tasks.splice(index, 1);
      }
    }
  }
  </script>
  
  <style>
  body {
    font-family: cursive;
    background-color: #A3966A;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }
  
  main {
    width: 100%;
    width: 600px;
    padding: 20px;
    border-radius: 10px;
    font-family:cursive;
  }
  
  .todo-container {
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0px 0px 10px #482E1D;
    background-color: #895D2B;
    font-family: cursive;
  }
  
  .todo-container h2 {
    color: #482E1D;
  }
  
  .todo-component input[type="text"] {
    width: calc(100% - 95px);
    padding: 10px;
    border: #482E1D;
    border-radius: 5px 0 0 5px;
    outline: none;
    color: #482E1D;
  }
  
  .todo-component button {
    padding: 10px 15px;
    margin: 0 5px;
    background-color: #482E1D;
    color: #F0DAAE;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    outline: none;
  }
  
  .todo-component button:hover {
    background-color: #90553C;
  }
  
  .task {
    display: flex;
    align-items: center;
    margin: 10px 0;
    padding: 10px;
    border-radius: 5px;
    background-color: #F0DAAE;
    color: #482E1D;
  }
  
  .task input[type="checkbox"] {
    margin-right: 10px;
  }
  
  .task-text {
    flex: 1;
    cursor: pointer;
    color: #482E1D;
    font-weight: bold;
  }
  
  .edit-input {
    flex: 1;
    margin-right: 10px;
    color: #482E1D;
  }
  
  .edit-mode {
    display: flex;
    align-items: center;
  }
  
  .button-group {
    display: flex;
    align-items: center;
  }
  
  .edit-btn, .delete-btn, .cancel-btn {
    margin-left: 5px;
  }
  
  .update-btn {
    margin-right: 5px;
  }
  
  .completed .task-text {
    text-decoration: line-through;
    opacity: 0.6;
  }
  
  .filter-btn {
    margin-top: 20px;
    padding: 10px 15px;
    background-color: #482E1D;
    color: #F0DAAE;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    outline: none;
  }
  
  .filter-btn:hover {
    background-color: #90553C;
  }
  
  .checkbox {
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    width: 15px;
    height: 15px;
    border: 1px solid #482E1D;
    border-radius: 5px;
    margin-right: 5px;
  }
  
  .checkbox:checked {
    background-color: #90553C;
  }
  </style>
  