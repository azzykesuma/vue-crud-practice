<template>
  <h1>Todo list</h1>
  <form>
    <label>Add todo</label>
    <input type="text" v-model= 'todo' />
    <button @click.prevent="handleAddTodo">Add Todo</button>
  </form>
  <div v-for="todo in todoData" key="todo.id">
    <TodoComponent :todo="todo" @delete="handleDelete"/>
  </div>
</template>

<script setup>
import { computed } from '@vue/reactivity';
import { ref } from 'vue';
import TodoComponent from './components/TodoComponent.vue'

const todoData = ref([])
const todoObj = ref({})
const todo = ref('')


  const handleAddTodo = () => {
   todoObj.value.id = todo.value
   todoObj.value.title = todo.value

   todoData.value = [...todoData.value, { 
      id : todoObj.value.id, 
      title : todoObj.value.title,
      isDone : false
    }]
  }

  const handleDelete = id => {
    todoData.value = todoData.value.filter(todo => todo.id !== id)
  }

  console.log(handleDelete);


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

