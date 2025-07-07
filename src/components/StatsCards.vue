<template>
  <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4 mb-6">
    <div
      v-for="(stat, index) in statsData"
      :key="index"
      class="rounded-xl border border-gray-200 dark:border-white/10 bg-white dark:bg-white/5 dark:backdrop-blur-md p-6 shadow-sm transition hover:shadow-md"
    >
      <div class="flex items-center gap-4">
        <component :is="stat.icon" class="w-10 h-10 text-blue-600 dark:text-blue-400" />

        <div>
          <h3 class="text-sm text-gray-500 dark:text-gray-300 font-medium">
            {{ stat.baslik }}
          </h3>
          <p class="text-2xl font-bold text-gray-900 dark:text-white">
            {{ stat.deger }}
          </p>
        </div>
      </div>

      <p
        class="mt-4 text-sm font-medium"
        :class="{
          'text-green-500': pozitifDegisimMi(stat.aciklama),
          'text-red-500': !pozitifDegisimMi(stat.aciklama)
        }"
      >
        {{ stat.aciklama }}
      </p>
    </div>
  </div>
</template>

<script setup>
import {
  UserGroupIcon,
  CurrencyDollarIcon,
  ShoppingCartIcon,
  BriefcaseIcon,
} from '@heroicons/vue/24/outline'
import { ref } from 'vue'

const statsData = ref([
  {
    baslik: 'Toplam Kullanıcı',
    deger: '1.212',
    aciklama: 'Geçen aya göre %14 artış',
    icon: UserGroupIcon,
  },
  {
    baslik: 'Gelir',
    deger: '₺12.450',
    aciklama: 'Geçen aya göre %23 artış',
    icon: CurrencyDollarIcon,
  },
  {
    baslik: 'Yeni Siparişler',
    deger: '320',
    aciklama: 'Geçen aya göre %4 azalış',
    icon: ShoppingCartIcon,
  },
  {
    baslik: 'Aktif Projeler',
    deger: '92',
    aciklama: 'Geçen aya göre %10 artış',
    icon: BriefcaseIcon,
  },
])

const pozitifDegisimMi = (aciklama) => aciklama.includes('artış')
</script>

