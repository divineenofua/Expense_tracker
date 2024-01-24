 <template>
    <form id="form" @submit.prevent='onSubmit'> 
    <div class="header-text">
        Add new transactions
    </div>
<div class="add-text">
    <label>Text</label> 
    
    <div class="input">
        <input type="text" v-model="text"   placeholder="Enter text..."/> 
     </div>
    
</div>
<div class="add-amount">
    <label>Amount <br />
    [negative - Expense , positive -income]</label> 
    
    <div class="input">
        <input type="text" v-model="amount" placeholder="Enter amount..">
      </div>
    
</div>
<div class="button">
    <button type="submit">Add transaction</button>
</div>
    </form>
 </template>


 <script setup>
 import { ref } from 'vue';
 import {useToast} from 'vue-toastification';

  const text = ref('');
  const amount = ref('');
  const toast = useToast();
  const emit = defineEmits(['transactionSubmitted']);
  const onSubmit = () => {
    if(!text.value || !amount.value) {
      toast.error('Please enter text and amount')
      return
    }
    const transData = {
        text: text.value,
        amount:parseFloat(amount.value)
    };
 console.log(text.value, amount.value)
    emit('transactionSubmitted', transData);
    // text.value ='';
    // amount.value='';
   }
</script>