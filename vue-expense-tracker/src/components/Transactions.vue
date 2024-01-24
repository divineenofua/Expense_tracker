<template>
    <div class="hist"> 
    <h3  >History</h3>
</div>
<div class="list"   >
    <div   :class="items.amount < 0 ? 'item minus' : 'item plus'" v-for=" items in TransactionsItem" :key="items.id" >
        <span>{{items.text}}</span>
        <span> ${{items.amount}}</span>
    </div>
    
</div>
</template>

<script setup>
import { defineProps } from 'vue';
const props = defineProps({
    TransactionsItem: {
        type: Array,
        required:true
    }
})
</script>