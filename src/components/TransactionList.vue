<template>
    <h3>History</h3>
    <ul id="list" class="list">
      <li v-for="transaction in props.transactions" :key="transaction.id" :class="transaction.amount > 0 ? 'plus' : 'minus'">
        {{ transaction.text }}<span>{{ transaction.amount }}</span><button @click="deleteTransaction(transaction.id)" class="delete-btn">x</button>
      </li>
    </ul>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import { defineProps } from 'vue';
  import { defineEmits } from 'vue';


  const props = defineProps({
    transactions :{
      type : Array , 
      required : true
    }

  });
  const emit = defineEmits(['deleteTransaction']);

  console.log(props.transactions);
  

  
  const deleteTransaction = (id) => {
    props.transactions = props.transactions.filter(transaction => transaction.id !== id);
    emit('deleteTransaction',props.transactions.value);
  }



  </script>
 
  