<template>
    <form @submit.prevent="handleSubmit">
        <input 
            type="text"
            placeholder="Hi, Jambi! you need to..."
            v-model="newTask"
        >
        <button>Add</button>
    </form>
</template>

<script>
import { useTaskStore } from '../store/TaskStore';
import { ref } from 'vue';

    export default {
        setup() {
            const taskStore = useTaskStore()
    
            const newTask = ref('')

            const handleSubmit = () => {
                if (newTask.value.length > 0) {
                    taskStore.addTask({
                        title: newTask.value,
                        isFav: false,
                        id: Math.floor(Math.random() * 10000) //With this way it can be repeated.
                    })
                    newTask.value = ''
                }
            }

            return {
                handleSubmit,
                newTask
            }
        }
    }
</script>