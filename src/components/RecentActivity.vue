<template>
  <div
    class="bg-white dark:bg-gray-900 shadow-lg rounded-lg p-6 border border-gray-200 dark:border-gray-700"
  >
    <h2 class="text-xl font-semibold mb-8 text-gray-900 dark:text-gray-100">
      Son Aktiviteler
    </h2>

    <ul class="relative border-l-2 border-primary dark:border-primary-dark">
      <li
        v-for="(activity, index) in recentActivities"
        :key="index"
        class="mb-10 ml-6"
      >
        <span
          class="absolute -left-3 flex items-center justify-center w-6 h-6 rounded-full bg-primary dark:bg-primary-dark ring-8 ring-white dark:ring-gray-900"
        >
          <Icon
            icon="line-md:circle-filled-to-confirm-circle-filled-transition"
            class="w-4 h-4 text-white"
          />
        </span>
        <div
          :class="[
            'p-4 rounded-md shadow-sm',
            index % 2 === 0
              ? 'bg-gray-100 dark:bg-gray-800 ml-8'
              : 'bg-gray-50 dark:bg-gray-700 ml-20',
          ]"
        >
          <h3 class="font-semibold text-lg text-gray-900 dark:text-gray-100">
            {{ activity.type }}
          </h3>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-1">
            {{ activity.time }}
          </p>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { Icon } from '@iconify/vue';

const recentActivities = ref([
  { type: 'Kullanıcı Girişi', time: '15:15' },
  { type: 'Yeni Sipariş', time: '15:20' },
  { type: 'Sistem Güncellemesi', time: '16:00' },
  { type: 'Kullanıcı Çıkışı', time: '16:15' },
  { type: 'Şifre Değiştirildi', time: '17:00' },
]);
</script>
