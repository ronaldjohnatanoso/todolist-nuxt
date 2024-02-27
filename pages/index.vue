<template>
    <div class="font-bold flex justify-center text-2xl m-20">
        TODO LIST using AI
    </div>
    <div class="flex justify-center space-x-4  ">
        <UTextarea @keydown.enter.prevent="handleAddTodo" v-model="inputTodo.text" class="w-1/2"
            placeholder="Enter whatever you want to do with your sorry life..." />
        <UButton @click="handleAddTodo" color="sky" class="w-20 flex justify-center">Imma do it later</UButton>
    </div>

    <div class="flex justify-center space-x-4 space-y-5 m-5" v-for="todo in todosArray">
        <div :style="{ 'text-decoration': todo.isFinished ? 'line-through' : 'none' }"
            class=" w-1/2 flex justify-center items-center ">{{ todo.text }}</div>
        <UButton @click="handleFinishNow(todo)" :color="todo.isFinished ? 'emerald' : 'rose'"
            class="h-20 w-20 flex justify-center"> {{ todo.isFinished ? 'Finish Na' : 'Dugaya gud mahuman' }}</UButton>
        <UButton @click="handleDelete(todo)" color="blue" class="h-20 w-20 flex justify-center"> Good Bye Forever </UButton>


    </div>
    <UDivider class="my-5"
    :avatar="{ src: 'https://avatars.githubusercontent.com/ronaldjohnatanoso' }"
  />
    <div class="flex justify-center ">
        <div class="m-5">Experimental features:</div>
  <div class="m-5">(Disabled) This app predicts your future and will automatically add todo tasks for you. Each todo task is a prophecy. </div>

    </div>
  
</template>

<script lang="ts" setup>
import { ref } from 'vue';

interface todoTask {
    text: string;
    isFinished: boolean;
}

const inputTodo = ref<todoTask>({ text: "", isFinished: false });
const todosArray = ref<todoTask[]>([]);

const handleFinishNow = (todo: todoTask) => {
    todo.isFinished = !todo.isFinished
}

const handleDelete = (todo: todoTask) => {
    const index = todosArray.value.indexOf(todo);
    if (index !== -1) {
        todosArray.value.splice(index, 1);
    }
}
const handleAddTodo = () => {
    //check if empty
    if (inputTodo.value.text === "") {
        return;
    }
    todosArray.value.push({ ...inputTodo.value }); // Push a new object with text and isFinished properties
    inputTodo.value.text = ""; // Clear the input
};
</script>

<style>
html,
body {
    height: 100%;
}

body {
    margin: 0;
    background-image: linear-gradient(to left, #81a5d7, #d07f8a, #b15fc8);
}
</style>