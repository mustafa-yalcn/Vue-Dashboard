<template>
  <div class="p-6 bg-white dark:bg-zinc-900 rounded-xl shadow-md h-[400px]">
    <h2 class="text-xl font-semibold mb-4 text-gray-800 dark:text-gray-100">
      Bölge Bazında Ürün Performansı
    </h2>
    <Bar :data="chartData" :options="chartOptions" />
  </div>
</template>

<script setup>
import { Bar } from 'vue-chartjs'
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale,
} from 'chart.js'

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

const chartData = {
  labels: ['1. Çeyrek', '2. Çeyrek', '3. Çeyrek', '4. Çeyrek'],
  datasets: [
    {
      label: 'Kuzey',
      data: [2400, 2900, 4200, 4600],
      backgroundColor: '#6366f1', 
      stack: 'Bölge',
    },
    {
      label: 'Güney',
      data: [3200, 3100, 4000, 5000],
      backgroundColor: '#f59e0b', 
      stack: 'Bölge',
    },
    {
      label: 'Doğu',
      data: [1800, 2500, 3000, 3500],
      backgroundColor: '#10b981',
      stack: 'Bölge',
    },
    {
      label: 'Batı',
      data: [2200, 2700, 3600, 4200],
      backgroundColor: '#ef4444',
      stack: 'Bölge',
    },
  ],
}

const chartOptions = {
  responsive: true,
  maintainAspectRatio: false,
  plugins: {
    legend: {
      position: 'top',
      labels: {
        color: '#94a3b8',
        boxWidth: 12,
        usePointStyle: true,
      },
    },
    tooltip: {
      callbacks: {
        afterLabel(context) {
          const total = context.dataset.data.reduce((a, b) => a + b, 0)
          const percent = ((context.raw / total) * 100).toFixed(1)
          return `Katkı: %${percent}`
        },
      },
    },
  },
  scales: {
    x: {
      stacked: true,
      ticks: {
        color: '#94a3b8',
      },
      grid: {
        display: false,
      },
    },
    y: {
      stacked: true,
      ticks: {
        color: '#94a3b8',
        callback: (value) => `${value}₺`, 
      },
      grid: {
        color: 'rgba(203, 213, 225, 0.2)',
      },
    },
  },
}
</script>
