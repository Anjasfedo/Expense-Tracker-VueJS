<script setup lang="js">
import { defineProps } from 'vue';

// Prop totalExpense and totalIncome from parent component.
const props = defineProps({
    totalExpense: {
        type: String,
        required: true,
    },
    totalIncome: {
        type: String,
        required: true,
    },
});


</script>

<template lang="html">
    <div class="">
        <div class="flex justify-evenly font-semibold text-center text-lg">
            <div class="px-8 py-4 rounded-lg border-2 border-gray-500 hover:bg-green-500 bg-gray-100">
                <h1 class="font-bold">Income</h1>
                <h1 class="text-green-800">${{ totalIncome }}</h1>
            </div>
            <div class="px-8 py-4 rounded-lg border-2 border-gray-500 hover:bg-red-500 bg-gray-100">
                <h1 class="font-bold">Expense</h1>
                <h1 class="text-red-800">${{ totalExpense }}</h1>
            </div>
        </div>
    </div>
</template>
  
<style lang="css">

</style>
