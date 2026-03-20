<template>
  <div class="card">
    <div class="card-header d-flex justify-content-between align-items-center">
      <h5 class="mb-0">История операций</h5>
      <span class="badge bg-secondary">{{ transactions.length }}</span>
    </div>
    <div class="card-body">
      <div v-if="transactions.length === 0" class="text-center text-muted py-4">
        Нет операций. Добавьте первую!
      </div>

      <ul class="list-group list-group-flush" v-else>
        <li 
          v-for="transaction in transactions" 
          :key="transaction.id"
          class="list-group-item d-flex justify-content-between align-items-center"
        >
          <div>
            <div class="fw-bold">{{ transaction.description }}</div>
            <small class="text-muted">
              {{ getCategoryName(transaction.category) }}
            </small>
          </div>
          
          <div class="d-flex align-items-center gap-3">
            <span 
              class="fw-bold"
              :class="transaction.type === 'income' ? 'text-success' : 'text-danger'"
            >
              {{ transaction.type === 'income' ? '+' : '-' }}
              {{ transaction.amount }} ₽
            </span>
            
            <button 
              @click="emit('delete-transaction', transaction.id)"
              class="btn btn-sm btn-outline-danger"
            >
              ✕
            </button>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
defineProps({
  transactions: {
    type: Array,
    required: true
  }
})

const emit = defineEmits(['delete-transaction'])

const categories = {
  food: '🍔 Еда',
  transport: '🚗 Транспорт',
  salary: '💼 Зарплата',
  entertainment: '🎬 Развлечения',
  other: '📦 Другое'
}

const getCategoryName = (key) => {
  return categories[key] || key
}
</script>