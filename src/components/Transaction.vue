<template>
  <h3>History</h3>
  <p v-if="transactionList.length === 0">No transactions added yet</p>
  <ul id="list" class="list">
    <li
      v-for="t in transactionList"
      :key="t.id"
      :class="t.amount < 0 ? 'minus' : 'plus'">
      {{ t.text }} <span>${{ t.amount }}</span>
      <button class="delete-btn" @click="deleteTransaction(t.id)">x</button>
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

const emit = defineEmits(["transactionDeleted"]);

const deleteTransaction = (id) => {
  emit("transactionDeleted", id);
};
</script>

<style lang="scss" scoped></style>
