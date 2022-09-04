<template>
    <div class="todo__wrapper">
        <input type="checkbox" v-model="check" @change="handleChange">
        <h3 :class="{done : props.todo.isDone}">{{ props.todo.title}}</h3>
        <div class="todo__button__wrapper">
            <button @click="openModal">edit</button>
            <button @click="handleDeleteEmit(props.todo.id)">delete</button>
        </div>
    </div>
        <div v-if="openEditModal">
            <Teleport to="body">
                <Modal 
                :open='openEditModal' 
                @close='handleModalClose'
                @submit="handleSubmit"
                :todo="todo"
                />
            </Teleport>
        </div>
</template>

<script setup>
import { ref } from 'vue';
import Modal from './EditModal.vue';

    const props = defineProps(['todo'])
    const emit = defineEmits(['delete'])
    const check = ref(false)
    const openEditModal = ref(false)

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

    const openModal = () => {
        openEditModal.value = true
        console.log(openEditModal.value);
    }

    const handleModalClose = () => {
        openEditModal.value = false
    }

    const handleSubmit = (payload,id) => {
        props.todo.id = payload
        props.todo.title = payload
        openEditModal.value = false
    }

</script>

<style scoped>
    .todo__wrapper {
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 10px;
        background-color: #778DA9;
        padding : 10px;
        border-radius: 5px;
        margin-block : 10px;
        animation-name: fade-in;
        animation-duration: .4s;
    }

    @keyframes fade-in {
        from { opacity: 0;}
        to { opacity: 1;}
    }

    h3 {
        color : #fafafa;
    }

    .todo__button__wrapper {
        display: flex;
        gap : 5px;
    }

    .done {
        text-decoration:line-through;
        opacity : 0.5;
    }

</style>