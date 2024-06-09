<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";

import { ref, computed } from 'vue';




const dummyTransactions = ref([
  { id: 1, text: "Flower", amount: -20 },
  { id: 2, text: "Salary", amount: 300 },
  { id: 3, text: "Book", amount: -10 },
  { id: 4, text: "Camera", amount: 150 },
]);

const checker = () => {
  console.log(dummyTransactions.value);
}


const totalBalance = computed(() => {

  let total = 0;
  dummyTransactions.value.forEach(element => {
    total += element.amount;
  });
  return total;
});


const income = computed ( () => {
  let income = 0;
  dummyTransactions.value.forEach(element => {
    if(element.amount > 0){
      income += element.amount;
    }
  });
  return income;
}); 


const expense = computed ( () => {
  let expense = 0;
  dummyTransactions.value.forEach(element => {
    if(element.amount < 0){
      expense += element.amount;
    }
  });
  return expense;
});


const addTransaction = (transaction) => {
  dummyTransactions.value.push(transaction);
}

</script>

<template>
  <Header />
  <div class="container">
    <Balance :balance="totalBalance" />
    <IncomeExpenses :income="income"  :expense="expense"/>
    <TransactionList :transactions="dummyTransactions" @deleteTransaction="checker" />
    <AddTransaction @transactionAdded="addTransaction"/>
  </div>
</template>
