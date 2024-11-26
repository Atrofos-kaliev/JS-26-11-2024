<script setup>
import { ref, computed } from "vue";
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

const nameLastname = ref('');
const date = ref('');
const days = ref('');
const salary = ref('');

const addPerson = () => {
  if (nameLastname.value && date.value && days.value && salary.value) {
    people.value.push({
    id: Date.now(),
    nameLastname: nameLastname.value,
    date: date.value,
    days: days.value,
    salary: parseFloat(salary.value),
    })

    nameLastname.value = '';
    date.value = '';
    days.value = '';
    salary.value = '';
  }
}

const removePerson = (id) => {
  people.value = people.value.filter(person => person.id !== id);
}

const totalSalary = computed(() => {
  return people.value.reduce((sum, person) => sum + person.salary, 0);
});

const totalSalaryWithNalog = computed(() => {
  return people.value.reduce((sum, person) => sum + (person.salary * 0.85), 0);
});

</script>

<template>
  <h2>Форма для заполнения</h2>
<div class="container">
  <div class="row">
    <div class="col">

      <div class="mb-3">
        <label for="nameLastname" class="form-label">Ф.И.О</label>
        <input type="text" class="form-control" id="namelastname" v-model="nameLastname" :class="{'is-invalid': !nameLastname}">
        <div class="invalid-feedback">
    Заполните Ф.И.О
      </div>
      </div>

      <div class="mb-3">
        <label for="date" class="form-label">Дата выдачи зарплаты</label>
        <input type="date" class="form-control" id="date" v-model="date" :class="{'is-invalid': !date}">
        <div class="invalid-feedback">
    Заполните дату выдачи зарплаты
      </div>
      </div>

      <div class="mb-3">
        <label for="days" class="form-label">Количество отработанных дней</label>
        <input type="number" class="form-control" id="days" v-model="days" :class="{'is-invalid': !days}">
        <div class="invalid-feedback">
    Заполните количество отработанных дней
      </div>
      </div>

      <div class="mb-3">
        <label for="salary" class="form-label">Размер заработной платы сотрудника</label>
        <input type="number" class="form-control" id="salary" v-model="salary" :class="{'is-invalid': !salary}">
        <div class="invalid-feedback">
    Заполните размер заработной платы сотрудника
      </div>
      </div>
      <button type="button" class="btn btn-primary" @click="addPerson">Добавить</button>
      
    </div>
    
  </div>
  <div class="mt-4">
    <h2>Список сотрудников</h2>
<div class="row row-cols-1 row-cols-md-2 g-4">
<div class="col" v-for="(person, index) in people" :key="person.id">
<div class="card h-100">
<div class="card-body">
  <h5 class="card-title">{{ index + 1 }}. {{ person.nameLastname }}</h5>
  <p class="card-text">Дата выдачи: {{ person.date }}</p>
  <p class="card-text">Отработанные дни: {{ person.days }}</p>
  <p class="card-text">Зарплата: ${{ person.salary }}</p>
  <p class="card-text">Зарплата с налогами: ${{ (person.salary * 0.85).toFixed(2) }}</p>
</div>
<div class="card-footer text-end">
  <button class="btn btn-outline-danger" @click="removePerson(person.id)">Удалить</button>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="mt-4">
  <h5>Общая зарплата: ${{ totalSalary }}</h5>
  <h5>Общая зарплата с налогом (15%): ${{ totalSalaryWithNalog }}</h5>
  </div>
</template>