<template>
    <div class="mt-4">
      <h5>Общая зарплата: ${{ totalSalary.toFixed(2) }}</h5>
      <h5>Общая зарплата с налогом (15%): ${{ totalSalaryWithNalog.toFixed(2) }}</h5>
    </div>
  </template>
  
  <script setup>
  const props = defineProps({
    totalSalary: Number,
    totalSalaryWithNalog: Number,
  });
  </script>  