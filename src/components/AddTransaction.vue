<template>
  <h3>Add new transaction</h3>
  <form @submit.prevent="onSubmit" id="form">
    <div class="form-control">
      <label for="text">Text</label>
      <input v-model="inputText" type="text" id="text" placeholder="Enter text..." />    
    </div>
    <div class="form-control">
      <label for="amount"
        >Amount <br />
        (negative - expense, positive - income)</label
      >
      <input v-model="inputAmount" type="number" id="amount" placeholder="Enter amount..." />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>


<script setup>

import { ref } from 'vue'; 

import { useToast } from "vue-toastification";
import {defineEmits}  from 'vue';

const inputText = ref('');
const inputAmount = ref(0); 

const emit = defineEmits(['transactionAdded'])
const toast = useToast(); 

const onSubmit = () => {
  console.log(inputText.value);
  console.log(inputAmount.value);
  if(inputText.value.trim() === '' || inputAmount.value === 0){
    toast.error('Please enter valid text and amount');
    return;
  }
 
  const transaction = {
    id : Math.floor(Math.random() * 100000000),
    text : inputText.value,
    amount : +inputAmount.value
  }

  emit('transactionAdded',transaction); 
  inputText.value = '';
  inputAmount.value = 0;  
}


</script>
