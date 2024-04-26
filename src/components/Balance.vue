<template>
  <h4>Your Balance</h4>
  <h5 id="balance">${{ total }}</h5>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
  total: {
    type: Number,
    required: true,
  },
});
</script>

<style lang="scss" scoped></style>
