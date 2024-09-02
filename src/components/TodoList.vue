<template>
    <!-- Main container for the todo list -->
    <div class="todo-container">
      <h1>Todo-lista</h1>
  
      <!-- Input group to add new tasks -->
      <div class="input-group">
        <!-- v-model binds the input field value to the 'newTodo' reactive variable -->
        <input type="text" v-model="newTodo" placeholder="Lägg till en ny uppgift" />
        <!-- @click is a Vue event handler that triggers the 'addTodo' method when the button is clicked -->
        <button @click="addTodo">Lägg till</button>
      </div>
  
      <!-- List of todo items -->
      <ul class="todo-list">
        <!-- v-for directive loops through each item in the 'todos' array -->
        <!-- :key ensures that each list item has a unique identifier for efficient rendering -->
        <!-- :class applies the 'completed' class conditionally based on the 'completed' property of each todo item -->
        <li v-for="todo in todos" :key="todo.id" :class="{ completed: todo.completed }">
          <!-- Clicking the span toggles the completion state of the todo item -->
          <span @click="toggleComplete(todo)">{{ todo.title }}</span>
          <!-- Button to remove the todo item, triggers the 'removeTodo' method -->
          <button @click="removeTodo(todo)">Ta bort</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  // Importing 'ref' from Vue's Composition API to create reactive references
  import { ref } from 'vue';
  
  export default {
    // Setup function is used to define reactive data and methods
    setup() {
      // 'newTodo' is a reactive variable to hold the new task text
      const newTodo = ref('');
      // 'todos' is a reactive array to store all tasks
      const todos = ref([]);
  
      // Method to add a new todo item
      const addTodo = () => {
        // Check if the input field is not empty
        if (newTodo.value.trim() !== '') {
          // Add a new todo object to the 'todos' array with a unique id, title, and completion status
          todos.value.push({ id: Date.now(), title: newTodo.value, completed: false });
          // Reset the input field
          newTodo.value = '';
        }
      };
  
      // Method to toggle the completed state of a todo item
      const toggleComplete = (todo) => {
        // Toggle the 'completed' boolean property
        todo.completed = !todo.completed;
      };
  
      // Method to remove a todo item from the list
      const removeTodo = (todo) => {
        // Filter out the todo item that matches the given id
        todos.value = todos.value.filter(t => t.id !== todo.id);
      };
  
      // Returning reactive variables and methods to the template
      return {
        newTodo,      // The input field data
        todos,        // The list of todo items
        addTodo,      // Method to add a new task
        toggleComplete, // Method to toggle the completed state
        removeTodo    // Method to remove a task
      };
    }
  };
  </script>
  
  <style scoped>
  /* Styles specific to this component are scoped to prevent conflicts with other styles */
  
  /* Main container styles */
  .todo-container {
    max-width: 600px;    /* Maximum width for the container */
    margin: 0 auto;      /* Center the container horizontally */
    padding: 20px;       /* Padding around the content */
    text-align: center;  /* Center the text */
  }
  
  /* Styles for the input group */
  .input-group {
    display: flex;       /* Display input and button in a row */
    justify-content: center; /* Center the input group horizontally */
    margin-bottom: 20px; /* Space below the input group */
  }
  
  /* Input field styles */
  .input-group input {
    width: 60%;          /* Width of the input field */
    padding: 10px;       /* Padding inside the input field */
    font-size: 16px;     /* Font size for the input text */
  }
  
  /* Add button styles */
  .input-group button {
    padding: 10px;       /* Padding inside the button */
    font-size: 16px;     /* Font size for the button text */
    margin-left: 10px;   /* Space between the input field and button */
  }
  
  /* Todo list styles */
  .todo-list {
    list-style-type: none; /* Remove default list styling */
    padding: 0;            /* Remove padding */
  }
  
  /* Styles for each todo item */
  .todo-list li {
    padding: 10px;       /* Padding around each item */
    border-bottom: 1px solid #ccc; /* Line separating items */
    display: flex;       /* Display content in a row */
    justify-content: space-between; /* Space out text and buttons */
    align-items: center; /* Align items vertically */
  }
  
  /* Styles for completed tasks */
  .todo-list li.completed span {
    text-decoration: line-through; /* Strike-through text for completed tasks */
    color: gray;                   /* Gray color for completed tasks */
  }
  
  /* Clickable span styles */
  .todo-list li span {
    cursor: pointer;     /* Cursor changes to pointer on hover */
  }
  
  /* Remove button styles */
  .todo-list li button {
    background-color: red;  /* Red background for delete button */
    color: white;           /* White text color */
    border: none;           /* Remove button border */
    padding: 5px 10px;      /* Padding inside the button */
    cursor: pointer;        /* Cursor changes to pointer on hover */
  }
  </style>
  