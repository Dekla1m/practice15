<template>
  <div class="row mb-4">
    <div class="col-md-4">
      <div class="card text-white bg-primary mb-3">
        <div class="card-body">
          <h5 class="card-title">Общий баланс</h5>
          <h2 class="card-text">{{ formatMoney(balance) }}</h2>
        </div>
      </div>
    </div>
    <div class="col-md-4">
      <div class="card text-white bg-success mb-3">
        <div class="card-body">
          <h5 class="card-title">Доходы</h5>
          <h2 class="card-text">{{ formatMoney(income) }}</h2>
        </div>
      </div>
    </div>
    <div class="col-md-4">
      <div class="card text-white bg-danger mb-3">
        <div class="card-body">
          <h5 class="card-title">Расходы</h5>
          <h2 class="card-text">{{ formatMoney(expense) }}</h2>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  transactions: {
    type: Array,
    required: true
  }
})

// Вычисляемые свойства
const income = computed(() => {
  return props.transactions
    .filter(t => t.type === 'income')
    .reduce((sum, t) => sum + t.amount, 0)
})

const expense = computed(() => {
  return props.transactions
    .filter(t => t.type === 'expense')
    .reduce((sum, t) => sum + t.amount, 0)
})

const balance = computed(() => {
  return income.value - expense.value
})

// Форматирование денег
const formatMoney = (amount) => {
  return new Intl.NumberFormat('ru-RU', {
    style: 'currency',
    currency: 'RUB'
  }).format(amount)
}
</script>