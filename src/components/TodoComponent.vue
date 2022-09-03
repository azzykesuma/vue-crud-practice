<template>
    <div class="todo__wrapper">
        <input type="checkbox" v-model="check" @change="handleChange">
        <h3 :class="{done : props.todo.isDone}">{{ props.todo.title}}</h3>
        <div class="todo__button__wrapper">
            <button>edit</button>
            <button @click="handleDeleteEmit(props.todo.id)">delete</button>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

    const props = defineProps(['todo'])
    const emit = defineEmits(['delete'])
    const check = ref(false)

    const handleChange = () => {
        if(check.value === true) {
            props.todo.isDone = true
        }
        else {
            props.todo.isDone = false
        }
    }

    const handleDeleteEmit = id => {
        emit('delete', id)
    }
</script>

<style scoped>
    .todo__wrapper {
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 10px;
    }

    .todo__button__wrapper {
        display: flex;
        gap : 5px;
    }

    .done {
        text-decoration:line-through;
    }
</style>