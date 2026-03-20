<template>
  <div class="container py-5">
    <h1 class="text-center mb-4">Трекер Расходов</h1>
    
    <!-- Блок баланса -->
    <BalanceCard 
      :transactions="transactions" 
    />

    <div class="row mt-4">
      <!-- Форма добавления -->
      <div class="col-md-4 mb-3">
        <TransactionForm 
          @add-transaction="addTransaction" 
        />
      </div>

      <!-- Список транзакций -->
      <div class="col-md-8">
        <TransactionList 
          :transactions="transactions"
          @delete-transaction="deleteTransaction"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, watch } from 'vue'
import BalanceCard from './components/BalanceCard.vue'
import TransactionForm from './components/TransactionForm.vue'
import TransactionList from './components/TransactionList.vue'

// Состояние
const transactions = ref([])

// Загрузка из localStorage при старте
onMounted(() => {
  const saved = localStorage.getItem('transactions')
  if (saved) {
    transactions.value = JSON.parse(saved)
  }
})

// Сохранение при изменениях
watch(transactions, (newVal) => {
  localStorage.setItem('transactions', JSON.stringify(newVal))
}, { deep: true })

// Добавить транзакцию
const addTransaction = (transaction) => {
  transactions.value.unshift({
    id: Date.now(),
    ...transaction
  })
}

// Удалить транзакцию
const deleteTransaction = (id) => {
  transactions.value = transactions.value.filter(t => t.id !== id)
}
</script>