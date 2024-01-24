<template>
    <div class="container">
        <div class="income">
            <p>INCOME</p>
            <span class="plus">+${{incomeTotal}}</span>
        </div>
        <div class="expense">
            <p>EXPENSE</p>
            <span class="minus">${{expenseTotal}}</span>
        </div>
    </div>
</template>

<script setup>
import { defineProps } from 'vue';
 const props = defineProps({
    expenseTotal: {
        type: Number,
        required: true
    },
    incomeTotal: {
        type: Number,
        required:true
    }
 })
</script>