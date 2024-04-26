<script setup>
import { ref, computed } from "vue";
import { useToast } from "vue-toastification";

import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpense from "./components/IncomeExpense.vue";
import Transaction from "./components/Transaction.vue";
import AddTransaction from "./components/AddTransaction.vue";

const toast = useToast();

const dummyTransactions = [
  { id: 1, text: "Flower", amount: -20 },
  { id: 2, text: "Salary", amount: 300 },
  { id: 3, text: "Book", amount: -10 },
  { id: 4, text: "Camera", amount: 150 },
];

const transactionList = ref(dummyTransactions);

// Get Total
const total = computed(() => {
  return transactionList.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0);
});

// Get total income
const totalIncome = computed(() => {
  return transactionList.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

// Get total expense
const totalExpense = computed(() => {
  return transactionList.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

const handleTransactionSubmit = (transactionData) => {
  transactionList.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount,
  });
  // console.log(transactionData);

  toast.success("Transaction added successfully");
};

// Generate unique ID
const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000);
};
</script>

<template>
  <Header />
  <div class="container">
    <Balance :total="+total" />
    <IncomeExpense :income="+totalIncome" :expense="+totalExpense" />
    <Transaction :transactionList="transactionList" />
    <AddTransaction @transactionSubmit="handleTransactionSubmit" />
  </div>
</template>

<style lang="scss" scoped></style>
