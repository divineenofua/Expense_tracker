
 
<template>
    <Header  :total = '+total' />
    <IncomeExpense :expenseTotal ='+expenseTotal' :incomeTotal ='+incomeTotal'  />
    <Transactions :TransactionsItem ='TransactionsItem' />
    <AddTransaction @transactionSubmitted="handleTransSubmitted" />
</template>



 <script setup>
 import Header from './components/Header.vue';
 import IncomeExpense from './components/IncomeExpense.vue';
 import Transactions from './components/Transactions.vue';
 import AddTransaction from './components/AddTransaction.vue';

import { ref, computed } from  'vue';
const TransactionsItem = ref([
    {id:1, text: 'clothes', amount:-19.09},
    {id:2, text: 'salary', amount:100},
    {id:3, text: 'Groceries', amount:-25.97},
    {id:4, text: 'Gift', amount:30.01}
]);
const total = computed(() => {
    return TransactionsItem.value.reduce((acc, trans) => {
        return acc + trans.amount;
    },0)
});

const expenseTotal = computed(() => {
    return TransactionsItem.value.filter(trans =>  trans.amount < 0).reduce((acc, trans) => {
       return acc + trans.amount;
    },0).toFixed(2);
});
const incomeTotal = computed(() => {
    return TransactionsItem.value.filter(trans =>  trans.amount > 0).reduce((acc, trans) => {
       return acc + trans.amount;
    },0).toFixed(2);
});

const handleTransSubmitted = (transData) => {
console.log(TransactionsItem.value);
TransactionsItem.value.push({
    id:generateUniqueId(),
    text:transData.text,
    amount:transData.amount

})
}

const generateUniqueId  = () => {
    return Math.floor(Math.random() * 1000000);
}


 </script>