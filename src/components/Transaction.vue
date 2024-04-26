<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <li
      v-for="t in transactionList"
      :key="t.id"
      :class="t.amount < 0 ? 'minus' : 'plus'">
      {{ t.text }} <span>${{ t.amount }}</span>
      <button class="delete-btn">x</button>
    </li>
  </ul>
</template>

<script setup>
import { ref } from "vue";

const dummyTransactions = [
  { id: 1, text: "Flower", amount: -20 },
  { id: 2, text: "Salary", amount: 300 },
  { id: 3, text: "Book", amount: -10 },
  { id: 4, text: "Camera", amount: 150 },
];

const transactionList = ref(dummyTransactions);
</script>

<style lang="scss" scoped></style>
