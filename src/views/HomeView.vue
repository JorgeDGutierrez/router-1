<script setup>
import { useCounterStore } from "@/store/counter";
import { storeToRefs } from "pinia";

const useCounter = useCounterStore();
const { increment } = useCounter;

const { count, double } = storeToRefs(useCounter);
</script>

<template>
  <h1>Home</h1>
  <p>Count: {{ count }}</p>
  <p>Double: {{ double }}</p>
  <button @click="increment">Increment</button>
</template>
