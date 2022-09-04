<template>
    <div class="todoModal">
        <div class="modal">
            <label>Edit your todo</label>
            <input v-model="editTodo" type="text">
            <div class="button-wrapper">
                <button @click="handleEditSubmit(editTodo,props.todo.id)">edit</button>
                <button @click="handleModalClose">cancel</button>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
    const props = defineProps(['todo'])
    const emit = defineEmits(['close','submit'])
    const editTodo = ref(props.todo.title)

    const handleModalClose = () => {
        emit('close')
    }

    const handleEditSubmit = (payload,id) => {
        emit('submit', payload, id)
    }

</script>

<style scoped>
    .todoModal {
        background-color: aquamarine;
        position: absolute;
        top : 30%;
        left: 50%;
        transform: translate(-50%, -50%); 
        padding: 10px 30px;
        border-radius: 5px;
        animation-name: fade-in;
        animation-duration: .4s;
    }

    @keyframes fade-in {
        from { opacity: 0;}
        to { opacity: 1;}
    }

    .modal {
        text-align: center;
        display: flex;
        flex-direction: column;
        gap : 10px;
    }

    .modal .button-wrapper {
        display: flex;
        gap : 10px;
        justify-content: center;
    }
</style>