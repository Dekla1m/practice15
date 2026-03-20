<template>
  <div class="card">
    <div class="card-header">
      <h5>Новая операция</h5>
    </div>
    <div class="card-body">
      <form @submit.prevent="submitForm">
        <div class="mb-3">
          <label class="form-label">Описание</label>
          <input 
            v-model="form.description" 
            type="text" 
            class="form-control" 
            placeholder="Например: Зарплата"
            required
          >
        </div>

        <div class="mb-3">
          <label class="form-label">Сумма</label>
          <input 
            v-model.number="form.amount" 
            type="number" 
            class="form-control" 
            placeholder="0"
            min="1"
            required
          >
        </div>

        <div class="mb-3">
          <label class="form-label">Тип</label>
          <select v-model="form.type" class="form-select">
            <option value="income">Доход</option>
            <option value="expense">Расход</option>
          </select>
        </div>

        <div class="mb-3">
          <label class="form-label">Категория</label>
          <select v-model="form.category" class="form-select">
            <option value="food">🍔 Еда</option>
            <option value="transport">🚗 Транспорт</option>
            <option value="salary">💼 Зарплата</option>
            <option value="entertainment">🎬 Развлечения</option>
            <option value="other">📦 Другое</option>
          </select>
        </div>

        <button type="submit" class="btn btn-primary w-100">
          Добавить
        </button>
      </form>
    </div>
  </div>
</template>

<script setup>
import { reactive } from 'vue'

const emit = defineEmits(['add-transaction'])

const form = reactive({
  description: '',
  amount: '',
  type: 'expense',
  category: 'other'
})

const submitForm = () => {
  emit('add-transaction', { ...form })
  // Очистка формы
  form.description = ''
  form.amount = ''
  form.category = 'other'
}
</script>