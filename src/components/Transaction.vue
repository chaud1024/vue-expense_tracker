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
import { defineProps } from "vue";

const props = defineProps({
  transactionList: {
    type: Array,
    required: true,
  },
});
</script>

<style lang="scss" scoped></style>
