<template>
    <div>
      <EmployeeForm @add-person="addPerson" />
      <EmployeeList :people="people" @remove-person="removePerson" />
      <SalarySummary :total-salary="totalSalary" :total-salary-with-nalog="totalSalaryWithNalog" />
    </div>
  </template>
  
  <script setup>
  import { ref, computed } from "vue";
  import EmployeeForm from './EmployeeForm.vue';
  import EmployeeList from './EmployeeList.vue';
  import SalarySummary from './SalarySummary.vue';
  
  const people = ref([
    {
      id: 1,
      nameLastname: 'Владислав',
      date: "26.11.2024",
      days: 21,
      salary: 990,
    },
    {
      id: 2,
      nameLastname: 'Тамерлан',
      date: "01.12.2024",
      days: 31,
      salary: 1900,
    },
  ]);
  
  const addPerson = (person) => {
    people.value.push(person);
  };
  
  const removePerson = (id) => {
    people.value = people.value.filter(person => person.id !== id);
  };
  
  const totalSalary = computed(() => {
    return people.value.reduce((sum, person) => sum + person.salary, 0);
  });
  
  const totalSalaryWithNalog = computed(() => {
    return people.value.reduce((sum, person) => sum + (person.salary * 0.85), 0);
  });
  </script>