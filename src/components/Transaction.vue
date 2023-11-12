<script setup lang="js">

import { defineProps } from 'vue';

// Prop expense from parent component.
const props = defineProps({
    expense: {
    type: Array,
    required: true,
  },
});

// Inititlize emit to passing method to parent component.
const emit = defineEmits(['transactionDeleted']);

// Method submit delete passing data to parent component with emit. 
const submitDelete = (data) => {
    emit('transactionDeleted', data);
}

</script>

<template lang="html">
    <h1 class="text-2xl font-bold mt-8">History</h1>
    <ul v-for="data, index in expense" :key="index" class="flex flex-col gap-2 font-bold">
        <li v-if="data.amount < 0" class="bg-red-300 hover:bg-red-400 ring-2 p-1 rounded-md group relative flex justify-between px-6">
            {{ data.text }} <span class="rounded-xl px-1">-${{ Math.abs(data.amount) }}</span>
            <button @click="submitDelete(data)" class="hidden group-hover:inline-block right-1 absolute bg-red-600 rounded-md px-1">X</button>
        </li>

        <li v-else class="bg-green-300 hover:bg-green-400 ring-2 p-1 rounded-md group relative flex justify-between px-6">
            {{ data.text }} <span class="rounded-xl px-1">${{ data.amount }}</span>
            <button @click="submitDelete(data)" class="hidden group-hover:inline-block right-1 absolute bg-red-600 rounded-md px-1">X</button>
        </li>
    </ul>
</template>
  
<style lang="css">

</style>
