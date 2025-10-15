<template>
  <div class="chart-container">
    <h2 class="text-xl font-bold text-center mb-4 text-green-700">
      Data Produksi <span class="text-gray-800">Bayam</span>
    </h2>
    <Bar :data="chartData" :options="chartOptions" />
  </div>
</template>

<script lang="ts" setup>
import { Bar } from "vue-chartjs";
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale,
} from "chart.js";
import type { ChartOptions } from "chart.js"; // ✅ type-only import
import ChartDataLabels from "chartjs-plugin-datalabels";

// Registrasi komponen Chart.js
ChartJS.register(
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale,
  ChartDataLabels
);

// Data chart
const chartData = {
  labels: ["2020", "2021", "2022", "2023", "2024"],
  datasets: [
    {
      label: "Luas Panen",
      backgroundColor: "#3b82f6",
      data: [2158.46, 2164.87, 1647.18, 1452.56, 1438.83],
    },
    {
      label: "Produksi",
      backgroundColor: "#f97316",
      data: [11733.07, 12643.68, 8874.35, 12940.45, 11091.14],
    },
  ],
};

// ✅ chartOptions dengan type-safe
const chartOptions: ChartOptions<"bar"> = {
  responsive: true,
  maintainAspectRatio: false,
  plugins: {
    legend: {
      position: "top",
      labels: { color: "#333", font: { size: 12 } },
    },
    title: { display: false },
    datalabels: {
      color: "#111",
      anchor: "end",
      align: "start",
      formatter: (value: number) =>
        value.toLocaleString("id-ID", { minimumFractionDigits: 2 }),
      font: { size: 11, weight: "bold" },
    },
  },
  scales: {
    x: {
      ticks: { color: "#444", font: { size: 12 } },
      grid: { display: false },
    },
    y: {
      beginAtZero: true,
      ticks: {
        color: "#444",
        callback: (value: any) =>
          value.toLocaleString("id-ID", { minimumFractionDigits: 0 }),
      },
      grid: { color: "#ddd" },
    },
  },
};
</script>

<style scoped>
.chart-container {
  background: linear-gradient(to right, #ecfdf5, #f0fdf4);
  border-radius: 1rem;
  padding: 1.5rem;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
  height: 420px;
  width: 100%;
  max-width: 800px;
  margin: 0 auto;
}
</style>
