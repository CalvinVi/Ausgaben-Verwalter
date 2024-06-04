<template>My App
<Header/>
<div class="container">
  <Balance :total="total" />
  <IncomeExpenses />
  <TransactionList :transactions="transactions"/>
  <AddTransaction/>
</div>
</template>



<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from "@/components/AddTransaction.vue";
import axios from 'axios';
const message = ref('');

const fetchHello = () => {
  axios.get(import.meta.env.VITE_BACKEND_URL + '/hello', {
    params: { text: 'Test' }
  })
      .then(function (response) {
        // handle success
        console.log(response);
        message.value = response.data;
      })
      .catch(function (error) {
        // handle error
        console.log(error);
      })
      .finally(function () {
        // always executed
      });
};

import { ref, computed } from 'vue';

const transactions = ref ([
  { id:1, text:'Flower',amount: 10.00},
  { id:2, text:'Salary',amount: 100.00},
  { id:3, text:'Book',amount: -10.00},
  { id:4, text:'Camera',amount: -10.00},
]);
const total= computed(() => {
  return transactions.value.reduce((acc, transaction) =>{
    return acc+transaction.amount;
    },0);
});
</script>