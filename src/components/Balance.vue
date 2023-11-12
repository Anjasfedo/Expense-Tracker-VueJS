<script setup lang="js">
import { defineProps } from 'vue';

// Prop totalBalance that get from parent component.
const props = defineProps({
    totalBalance: {
    type: String,
    required: true,
  },
});
</script>

<template lang="html">
    <div class="text-3xl font-bold py-5 mt-8">
        <h1>Your Balance</h1>
        <h1>${{ totalBalance }}</h1>
    </div>
</template>
  
<style lang="css">

</style>
