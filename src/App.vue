<script setup>
// Import components.
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpense from './components/IncomeExpense.vue';
import Transaction from './components/Transaction.vue';
import AddTransaction from './components/AddTransaction.vue';

// Import ref, watchEffect, and computed from vue.
import { ref, watchEffect, computed } from 'vue';

// Initialize constant variable for storage key.
const STORAGE_KEY = 'vue-expense-tracker'

// Use local storage as variable of expense.
const expense = ref(JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]'))

// Persist state, recycle (set item -> do rerender every expense change).
watchEffect(() => {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(expense.value))
})

// Method for Add Transaction, that get emit from child component.
const handleTransactionSubmitted = (data) => {
  expense.value.push(data)
}

// Delete Transaction method, that also get emit form child component.
const handleTransactionDeleted = (data) => {
  expense.value = expense.value.filter((ele) => ele != data)
}

// Total Balance from amount value from expense.
const totalBalance = computed(() => {
  return expense.value.reduce((acc, ele) => acc + ele.amount, 0).toFixed(2);
})

// Total Expense only amount value from expense that less than 0(negative number).
const totalExpense = computed(() => {
  return expense.value.filter((ele) => ele.amount < 0).reduce((acc, ele) => acc + ele.amount, 0).toFixed(2);
})

// Total Income get amount value from expense that grater than 0(positive number)
const totalIncome = computed(() => {
  return expense.value.filter((ele) => ele.amount > 0).reduce((acc, ele) => acc + ele.amount, 0).toFixed(2);
})

</script>

<template>
  <div class="flex justify-center items-center h-fit py-10">
    <div class="bg-blue-100 h-5/6 w-2/6 flex flex-col items-center p-4 rounded-2xl ring-gray-600 ring-2">
      <Header />
      <div class="text-gray-800 flex flex-col w-full px-6 gap-4">
        <Balance :totalBalance="totalBalance" />
        <IncomeExpense :totalExpense="totalExpense" :totalIncome="totalIncome" />
        <Transaction :expense="expense" @transactionDeleted="handleTransactionDeleted" />
        <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
      </div>
      <button class="bg-red-600 w-fit p-2 rounded-md text-white hover:bg-red-900 ring-1 ring-gray-500" @click="expense = []">Clear All Data</button>
    </div>
  </div>
</template>

<style scoped></style>
