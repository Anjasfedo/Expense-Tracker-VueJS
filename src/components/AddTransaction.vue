<script setup lang="js">
import { ref } from 'vue';

// Variable inputUser to save input value.
const inputUser= ref({
    text: '',
    amount: '',
})

// Initialize emit for passing method to parent component.
const emit = defineEmits(['transactionSubmitted']);

// Method to submit input from user.
const submitInput = () => {
    if (!inputUser.value.text && !inputUser.value.amount) {
        alert('Please Input Text and Amount!!')
    } else if(!inputUser.value.text) {
        alert('Please Input Text!!')
    } else if (!inputUser.value.amount) {
        alert('Please Input Amount!!')
    } else {
        emit('transactionSubmitted', inputUser.value);
        inputUser.value = {
            text: '',
            amount: '',
        }
    }
}


</script>

<template lang="html">
    <h1 class="text-2xl font-bold mt-8">Add New Transaction</h1>
    <form  @submit.prevent="submitInput" class="flex flex-col gap-4 text-md font-semibold">
        <div class="flex flex-col gap-1">
            <label for="inputText">Text</label>
            <input v-model="inputUser.text" type="text" id="inputText" class="ring-blue-400 ring-1 rounded-lg p-1" placeholder="Enter Text...">
        </div>
        <div class="flex flex-col gap-1">
            <label for="inputAmount">Amount</label>
            <input v-model="inputUser.amount" type="number" id="inputAmount" class="ring-blue-400 ring-1 rounded-lg p-1" placeholder="Enter Amount...">
        </div>
        <button type="submit" class="bg-blue-500 hover:bg-blue-700 rounded-lg ring-gray-500 ring-2 w-fit p-2 self-center text-white my-8">Add Transaction</button>
    </form>
</template>
  
<style lang="css">

</style>
