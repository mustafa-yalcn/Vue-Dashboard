<template>
  <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
    <div
      class="bg-white dark:bg-gray-900 p-6 rounded-xl shadow-lg border border-gray-200 dark:border-gray-700"
    >
      <h2
        class="text-xl font-semibold mb-6 text-gray-900 dark:text-gray-100 tracking-wide"
      >
        Aylık Gelir
      </h2>
      <Line
        :data="lineChartData"
        :options="lineChartOptions"
        class="max-h-[320px]"
        :key="lineChartKey"
      />
    </div>

    <div
      class="bg-white dark:bg-gray-900 p-6 rounded-xl shadow-lg border border-gray-200 dark:border-gray-700"
    >
      <h2
        class="text-xl font-semibold mb-6 text-gray-900 dark:text-gray-100 tracking-wide"
      >
        Gelir Kaynakları
      </h2>
      <Doughnut
        :data="doughnutChartData"
        :options="doughnutChartOptions"
        class="max-h-[320px]"
        :key="doughnutChartKey"
      />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { Line, Doughnut } from "vue-chartjs";
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  LineElement,
  CategoryScale,
  LinearScale,
  PointElement,
  ArcElement,
} from "chart.js";

ChartJS.register(
  Title,
  Tooltip,
  Legend,
  LineElement,
  CategoryScale,
  LinearScale,
  PointElement,
  ArcElement
);

const lineChartKey = ref(0);
const doughnutChartKey = ref(0);

const lineChartData = ref({
  labels: ["Oca", "Şub", "Mar", "Nis", "May", "Haz"],
  datasets: [
    {
      label: "Gelir (₺)",
      data: [1200, 1900, 3000, 5000, 2000, 3000],
      fill: false,
      borderColor: "#E82561",
      backgroundColor: "#E82561",
      tension: 0.4,
      pointRadius: 5,
      pointHoverRadius: 7,
    },
  ],
});

const doughnutChartData = ref({
  labels: ["Ürünler", "Hizmetler", "Abonelik", "Danışmanlık"],
  datasets: [
    {
      data: [35, 25, 20, 20],
      backgroundColor: ["#463581", "#E82561", "#ECE852", "#FFA24C"],
      borderWidth: 0,
      hoverOffset: 30,
    },
  ],
});

const lineChartOptions = ref({
  responsive: true,
  maintainAspectRatio: false,
  animation: {
    duration: 1200,
    easing: "easeInOutQuart",
  },
  plugins: {
    legend: {
      labels: {
        color: "#64748b",
        font: { size: 14, weight: "600" },
      },
    },
    tooltip: {
      mode: "index",
      intersect: false,
      backgroundColor: "#1F2937",
      titleColor: "#FBBF24",
      bodyColor: "#F9FAFB",
      cornerRadius: 6,
      padding: 10,
    },
  },
  scales: {
    x: {
      grid: {
        color: "rgba(100, 116, 139, 0.2)",
      },
      ticks: {
        color: "#64748b",
        font: { size: 13 },
      },
    },
    y: {
      grid: {
        color: "rgba(100, 116, 139, 0.2)",
      },
      ticks: {
        color: "#64748b",
        font: { size: 13 },
        callback: (value) => `${value.toLocaleString()} ₺`,
      },
    },
  },
});

const doughnutChartOptions = ref({
  responsive: true,
  maintainAspectRatio: false,
  cutout: "65%",
  animation: {
    duration: 1200,
    easing: "easeOutQuart",
    animateScale: true,
    animateRotate: true,
  },
  plugins: {
    legend: {
      position: "right",
      labels: {
        color: "#64748b",
        font: { size: 14, weight: "600" },
        boxWidth: 14,
        padding: 20,
      },
    },
    tooltip: {
      callbacks: {
        label: (context) => `${context.label}: %${context.raw}`,
      },
      backgroundColor: "#1F2937",
      titleColor: "#FBBF24",
      bodyColor: "#F9FAFB",
      cornerRadius: 6,
      padding: 10,
    },
  },
});

onMounted(() => {
  lineChartKey.value++;
  doughnutChartKey.value++;
});
</script>
