<template>
  <h1>Todo list</h1>
  <form>
    <div class="input-wrapper">
      <label>Add todo</label>
      <input type="text" v-model= 'todo' />
    </div>
    <button @click.prevent="handleAddTodo">Add Todo</button>
  </form>
  <div v-for="todo in todoData" key="todo.id">
    <TodoComponent :todo="todo" @delete="handleDelete" />
  </div>
  <p class='error' v-if="error">Please type proper todo activity</p>
  <p v-if="todoData.length === 0">Start adding todo :)</p>
</template>

<script setup>
import { ref } from 'vue';
import TodoComponent from './components/TodoComponent.vue'

const todoData = ref([])
const todoObj = ref({})
const todo = ref('')
const error = ref(false)


  const handleAddTodo = () => {
    
    if(todo.value) {
     todoObj.value.id = todo.value
     todoObj.value.title = todo.value
     todoData.value = [...todoData.value, { 
        id : todoObj.value.id, 
        title : todoObj.value.title,
        isDone : false
      }]
      error.value = false
    } else {
      error.value = true
      console.log(error.value);
    }
    todo.value = ''
  }

  const handleDelete = id => {
    todoData.value = todoData.value.filter(todo => todo.id !== id)
  }
  
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Lato&display=swap');
  body, #app {
    font-family: 'Lato',sans-serif;
  }

  body {
    background-color: #fafafa;
  }

  #app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  }
  
  form {
    display: flex;
    align-items: flex-end;
    justify-content: center;
    gap : 10px;
  }

  .input-wrapper {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
  }

  label {
    font-size: 1.3em;
    margin-bottom: 4px;
  }

  input {
    padding : 5px;
    font-size: 1.1em; 
    font-family: 'Lato',sans-serif;
  }

  button {
    padding : 10px 15px;
    background-color: #009FB7;
    border: none;
    border-radius: 5px;
    color : #fafafa;
    font-weight: bold;
  }

  .error {
    color : red
  }
</style>

