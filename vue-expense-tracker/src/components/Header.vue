<template>
    <div  class="header"> 
    <h1 >Expense Tracker</h1>
     <div>
        <h3>YOUR BALANCE</h3>
        <span>${{total}}</span>
     </div>
    </div>
</template>

<script setup>
import { defineProps } from 'vue';
const props = defineProps({
    total: {
        type: Number,
        required: true
    }
})
</script>  