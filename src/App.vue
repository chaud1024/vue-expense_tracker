<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpense from "./components/IncomeExpense.vue";
import Transaction from "./components/Transaction.vue";
import AddTransaction from "./components/AddTransaction.vue";
</script>

<template>
  <Header />
  <div class="container">
    <Balance />
    <IncomeExpense />
    <Transaction />
    <AddTransaction />
  </div>
</template>

<style lang="scss" scoped></style>