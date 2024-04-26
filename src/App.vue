<script setup>
import { ref, computed, onMounted } from "vue";
import { useToast } from "vue-toastification";

import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpense from "./components/IncomeExpense.vue";
import Transaction from "./components/Transaction.vue";
import AddTransaction from "./components/AddTransaction.vue";

const toast = useToast();

const transactionList = ref([]);

onMounted(() => {
  const savedTransactionList = JSON.parse(
    localStorage.getItem("transactionList"),
  );

  if (savedTransactionList) {
    transactionList.value = savedTransactionList;
  }
});

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

// save item to localStorage
const saveTransaction = () => {
  localStorage.setItem(
    "transactionList",
    JSON.stringify(transactionList.value),
  );
};

const handleTransactionSubmit = (transactionData) => {
  transactionList.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount,
  });
  // console.log(transactionData);
  saveTransaction();
  toast.success("Transaction added successfully");
};

// Generate unique ID
const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000);
};

const handleTransactionDelete = (id) => {
  transactionList.value = transactionList.value.filter(
    (transaction) => transaction.id !== id,
  );
  saveTransaction();

  toast.success("Transaction deleted.");
};
</script>

<template>
  <Header />
  <div class="container">
    <Balance :total="+total" />
    <IncomeExpense :income="+totalIncome" :expense="+totalExpense" />
    <Transaction
      :transactionList="transactionList"
      @transactionDeleted="handleTransactionDelete" />
    <AddTransaction @transactionSubmit="handleTransactionSubmit" />
  </div>
</template>

<style lang="scss" scoped></style>
