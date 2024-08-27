<template>
    <h3>Add a New Transaction</h3>
    <form  class="form" @submit.prevent="onSubmit" >
        <div class="form-control">
            <label for="text">Text</label>
            <input type="text" id="text" v-model="text" placeholder="Enter your text...">
        </div>
        <div class="form-control">
            <label for="amount">Amount <br>( negative -expense, positive-income )</label>
            <input type="text" v-model="amount" id="amount" placeholder="Enter amount...">
        </div>
        <Button class="btn">Add Transaction</Button>
    </form>
</template>

<script setup >
import { useToast } from 'vue-toastification';
import { ref } from 'vue';

const text = ref('');
const amount = ref('');
const emit = defineEmits(['transactionsSubmitted'])

const toast = useToast();

const onSubmit =()=>{
    if(!text.value || !amount.value){
        toast.error('Both Fields are Required');
        return;
    }
    const transactionData ={
        text: text.value,
        amount: parseFloat(amount.value)
    }
    emit('transactionsSubmitted', transactionData)
    text.value =''
    amount.value=''
}
</script>