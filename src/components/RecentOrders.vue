<template>
  <div
    class="bg-white dark:bg-gray-900 shadow-lg rounded-lg p-6 border border-gray-200 dark:border-gray-700"
  >
    <h2 class="text-xl font-semibold mb-6 text-gray-900 dark:text-gray-100">
      Son Siparişler
    </h2>

    <div class="overflow-x-auto">
      <table class="min-w-full divide-y divide-gray-200 dark:divide-gray-700">
        <thead class="bg-gray-50 dark:bg-gray-800">
          <tr>
            <th
              scope="col"
              class="px-6 py-3 text-left text-xs font-medium text-gray-500 dark:text-gray-400 uppercase tracking-wider"
            >
              Sipariş No
            </th>
            <th
              scope="col"
              class="px-6 py-3 text-left text-xs font-medium text-gray-500 dark:text-gray-400 uppercase tracking-wider"
            >
              Müşteri
            </th>
            <th
              scope="col"
              class="px-6 py-3 text-left text-xs font-medium text-gray-500 dark:text-gray-400 uppercase tracking-wider"
            >
              Tarih
            </th>
            <th
              scope="col"
              class="px-6 py-3 text-left text-xs font-medium text-gray-500 dark:text-gray-400 uppercase tracking-wider"
            >
              Tutar
            </th>
            <th
              scope="col"
              class="px-6 py-3 text-left text-xs font-medium text-gray-500 dark:text-gray-400 uppercase tracking-wider"
            >
              Durum
            </th>
          </tr>
        </thead>

        <tbody class="bg-white dark:bg-gray-900 divide-y divide-gray-200 dark:divide-gray-700">
          <tr
            v-for="(order, index) in recentOrders"
            :key="index"
            class="hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors"
          >
            <td
              class="px-6 py-4 whitespace-nowrap text-sm text-gray-900 dark:text-gray-100 font-medium"
            >
              {{ order.id }}
            </td>
            <td
              class="px-6 py-4 whitespace-nowrap text-sm text-gray-700 dark:text-gray-300"
            >
              {{ capitalize(order.customer) }}
            </td>
            <td
              class="px-6 py-4 whitespace-nowrap text-sm text-gray-700 dark:text-gray-300"
            >
              {{ order.date }}
            </td>
            <td
              class="px-6 py-4 whitespace-nowrap text-sm text-gray-700 dark:text-gray-300"
            >
              {{ formatAmount(order.amount) }}
            </td>
            <td class="px-6 py-4 whitespace-nowrap">
              <span
                :class="[
                  'inline-flex items-center px-3 py-1 rounded-full text-xs font-semibold',
                  statusColors[getStatusClass(order.status)] || statusColors.neutral
                ]"
              >
                {{ order.status }}
              </span>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <div class="flex justify-end mt-6">
      <button
        class="bg-indigo-600 text-white px-4 py-2 rounded-md hover:bg-indigo-700 transition"
      >
        Hepsini Görüntüle
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const recentOrders = ref([
  {
    id: '12345',
    customer: 'ahmet',
    date: '06-07-2025',
    amount: 120.5,
    status: 'Tamamlandı',
  },
  {
    id: '12346',
    customer: 'ayşe',
    date: '06-06-2025',
    amount: 220,
    status: 'Beklemede',
  },
  {
    id: '12347',
    customer: 'mehmet',
    date: '06-05-2025',
    amount: 55.75,
    status: 'İptal Edildi',
  },
])

const statusColors = {
  success:
    'bg-green-100 text-green-800 dark:bg-green-900 dark:text-green-300',
  warning:
    'bg-yellow-100 text-yellow-800 dark:bg-yellow-900 dark:text-yellow-300',
  error: 'bg-red-100 text-red-800 dark:bg-red-900 dark:text-red-300',
  neutral:
    'bg-gray-100 text-gray-800 dark:bg-gray-800 dark:text-gray-300',
}

function getStatusClass(status) {
  const statusMap = {
    Tamamlandı: 'success',
    Beklemede: 'warning',
    'İptal Edildi': 'error',
  }
  return statusMap[status] || 'neutral'
}

function capitalize(text) {
  if (!text) return ''
  return text.charAt(0).toUpperCase() + text.slice(1)
}

function formatAmount(amount) {
  return `${amount.toFixed(2)} ₺`
}
</script>
