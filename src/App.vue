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
  dummyTransactions.forEach(element => {
    total += element.amount;
  });
  return total;
});


</script>

<template>
  <Header />
  <div class="container">
    <Balance :balance="totalBalance" />
    <IncomeExpenses />
    <TransactionList :transactions="dummyTransactions" @deleteTransaction="checker" />
    <AddTransaction />
  </div>
</template>
