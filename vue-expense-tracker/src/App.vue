
 
<template>
    <Header  :total = '+total' />
    <IncomeExpense :expenseTotal ='+expenseTotal' :incomeTotal ='+incomeTotal'  />
    <Transactions :TransactionsItem ='TransactionsItem' @transFilter="filterItem" />
    <AddTransaction @transactionSubmitted="handleTransSubmitted" />
</template>



 <script setup>
 import Header from './components/Header.vue';
 import IncomeExpense from './components/IncomeExpense.vue';
 import Transactions from './components/Transactions.vue';
 import AddTransaction from './components/AddTransaction.vue';

import { ref, computed, onMounted } from  'vue';
import { useToast} from 'vue-toastification';
const toast = useToast();
onMounted(() => {
    const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

    if(savedTransactions){
        TransactionsItem.value = savedTransactions;
    }
})
const TransactionsItem = ref([]);
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

});
saveTransToLocalStorage();
toast.success('Transaction Added');
}

const generateUniqueId  = () => {
    return Math.floor(Math.random() * 1000000);
}
 
const filterItem = (id) => {

TransactionsItem.value = TransactionsItem.value.filter((trans) => 
    trans.id !== id);
    
    saveTransToLocalStorage();
  toast.success('Transaction Removed');
}
// save to local storage

const saveTransToLocalStorage = () => {
    localStorage.setItem('transactions', JSON.stringify(TransactionsItem.value))
}
 </script> 