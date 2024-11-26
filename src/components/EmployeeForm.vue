<template>
    <div class="container">
      <h2>Форма для заполнения</h2>
      <div class="row">
        <div class="col">
          <div class="mb-3">
            <label for="nameLastname" class="form-label">Ф.И.О</label>
            <input type="text" class="form-control" v-model="nameLastname" :class="{'is-invalid': !nameLastname}" />
            <div class="invalid-feedback">Заполните Ф.И.О</div>
          </div>
  
          <div class="mb-3">
            <label for="date" class="form-label">Дата выдачи зарплаты</label>
            <input type="date" class="form-control" v-model="date" :class="{'is-invalid': !date}" />
            <div class="invalid-feedback">Заполните дату выдачи зарплаты</div>
          </div>
  
          <div class="mb-3">
            <label for="days" class="form-label">Количество отработанных дней</label>
            <input type="number" class="form-control" v-model="days" :class="{'is-invalid': !days}" />
            <div class="invalid-feedback">Заполните количество отработанных дней</div>
          </div>
  
          <div class="mb-3">
            <label for="salary" class="form-label">Размер заработной платы сотрудника</label>
            <input type="number" class="form-control" v-model="salary" :class="{'is-invalid': !salary}" />
            <div class="invalid-feedback">Заполните размер заработной платы сотрудника</div>
          </div>
  
          <button type="button" class="btn btn-primary" @click="onSubmit">Добавить</button>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from "vue";
  
  const nameLastname = ref('');
  const date = ref('');
  const days = ref('');
  const salary = ref('');
  
  const emit = defineEmits();
  
  const onSubmit = () => {
    if (nameLastname.value && date.value && days.value && salary.value) {
      emit('add-person', {
        id: Date.now(),
        nameLastname: nameLastname.value,
        date: date.value,
        days: Number(days.value),
        salary: parseFloat(salary.value),
      });
      nameLastname.value = '';
      date.value = '';
      days.value = '';
      salary.value = '';
    } else {
      alert('Заполните все поля!');
    }
  };
  </script>  