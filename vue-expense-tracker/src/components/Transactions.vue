<template>
    <div class="hist"> 
    <h3  >History</h3>
</div>
<div class="list"   >
    <div class="listItem" v-for=" items in TransactionsItem" :key="items.id" >
        <button @click="onClick(items.id)">X</button>
         <div :class="items.amount < 0 ? 'item minus' : 'item plus'"> 
        <span>{{items.text}}</span>
        <span> ${{items.amount}}</span>
    </div>
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
});
const emit = defineEmits(['transFilter']);

 const onClick = (id) => {
    emit('transFilter',  id);
 }
 
</script>