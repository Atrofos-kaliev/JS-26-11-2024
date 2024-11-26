<template>
    <div class="mt-4">
      <h2>Список сотрудников</h2>
      <div class="row row-cols-1 row-cols-md-2 g-4">
        <div class="col" v-for="(person, index) in people" :key="person.id">
          <div class="card h-100">
            <div class="card-body">
              <h5 class="card-title">{{ index + 1 }}. {{ person.nameLastname }}</h5>
              <p class="card-text">Дата выдачи: {{ person.date }}</p>
              <p class="card-text">Отработанные дни: {{ person.days }}</p>
              <p class="card-text">Зарплата: ${{ person.salary.toFixed(2) }}</p>
              <p class="card-text">Зарплата с налогами: ${{ (person.salary * 0.85).toFixed(2) }}</p>
            </div>
            <div class="card-footer text-end">
              <button class="btn btn-outline-danger" @click="removePerson(person.id)">Удалить</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  const props = defineProps({
    people: Array,
  });
  
  const emit = defineEmits();
  
  const removePerson = (id) => {
    emit('remove-person', id);
  };
  </script>
 