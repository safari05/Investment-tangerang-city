
<script setup lang="ts">
import {onMounted, ref } from 'vue'
import L from 'leaflet'
import 'leaflet/dist/leaflet.css'

interface Item {
  icon: string
  label: string
  bgColor: string
}

const items = ref<Item[]>([
  { icon: 'fas fa-globe', label: 'Komoditi Pariwisata', bgColor: 'bg-green-600' },
  { icon: 'fas fa-industry', label: 'Kawasan Industri', bgColor: 'bg-yellow-400' },
  { icon: 'fas fa-plane', label: 'Bandara', bgColor: 'bg-orange-500' },
  { icon: 'fas fa-school', label: 'Sarana Pendidikan', bgColor: 'bg-blue-700' },
  { icon: 'fas fa-hotel', label: 'Hotel', bgColor: 'bg-green-700' },
  { icon: 'fas fa-hospital', label: 'Rumah Sakit', bgColor: 'bg-yellow-400' }
]);

onMounted(() => {
  const map = L.map('map').setView([-2.5489, 118.0149], 15)

  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    maxZoom: 19,
    attribution: '&copy; OpenStreetMap contributors'
  }).addTo(map)

  // Contoh marker (Jakarta)
  L.marker([-6.1767, 106.6319])
    .addTo(map)
    .bindPopup('Kota Tangerang')
    .openPopup()
})

</script>

<template>
  <div class="container mx-auto p-4 grid grid-cols-12 gap-4">
    <!-- Kiri: daftar ikon dan teks -->
    <div class="col-span-4 bg-white rounded-lg shadow p-4">
      <div
        v-for="(item, index) in items"
        :key="index"
        class="flex items-center gap-4 mb-6 cursor-pointer"
      >
        <div
          :class="['p-3 rounded-full text-white', item.bgColor]"
          class="flex justify-center items-center w-12 h-12"
        >
          <i :class="item.icon" class="text-xl"></i>
        </div>
        <div>
          <div class="text-green-700 font-semibold text-sm">Rp 15 Triliun</div>
          <div class="text-gray-700 font-medium">{{ item.label }}</div>
        </div>
      </div>
    </div>

    <!-- Kanan: Map Leaflet -->
    <div class="col-span-8 h-[610px] bg-blue-200 rounded-lg overflow-hidden shadow">
      <div id="map" class="w-full h-full"></div>
    </div>
  </div>
</template>

<style scoped>
@import 'https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css';

#map {
  height: 100%;
  width: 100%;
}
</style>