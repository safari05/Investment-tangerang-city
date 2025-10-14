<script setup lang="ts">
import { onMounted, ref } from 'vue'
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
])

// Koordinat tengah Tangerang
const center = { lat: -6.1767, lng: 106.6319 }

// Fungsi bantu buat random sebaran di sekitar titik tengah
function getRandomOffset(maxOffset = 0.02) {
  return (Math.random() - 0.5) * maxOffset * 2
}

// Handler klik marker
function handleMarkerClick(name: string, type: string) {
  console.log(`Anda mengklik marker: ${name}\nKategori: ${type}`)
}

onMounted(() => {
  const map = L.map('map').setView([center.lat, center.lng], 12)

  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    maxZoom: 19,
    attribution: '&copy; OpenStreetMap contributors'
  }).addTo(map)

  // ======= Generate 3 titik per kategori =======
  const samplePoints: { lat: number; lng: number; type: string; name: string }[] = []
  items.value.forEach(item => {
    for (let i = 1; i <= 3; i++) {
      samplePoints.push({
        lat: center.lat + getRandomOffset(),
        lng: center.lng + getRandomOffset(),
        type: item.label,
        name: `${item.label} ${i}`
      })
    }
  })

  // ======= Tambahkan marker =======
  samplePoints.forEach(point => {
    const item = items.value.find(i => i.label === point.type)
    if (!item) return

    const icon = L.divIcon({
      html: `<div class="flex justify-center items-center w-8 h-8 rounded-full ${item.bgColor}">
               <i class="${item.icon}" style="color:white;font-size:14px;"></i>
             </div>`,
      className: 'custom-marker-icon',
      iconSize: [30, 30],
      iconAnchor: [15, 15],
    })

    const marker = L.marker([point.lat, point.lng], { icon })
      .addTo(map)
      .bindPopup(`<b>${point.name}</b><br>${point.type}`)

    // Klik marker → trigger popup dan fungsi Vue
    marker.on('click', () => handleMarkerClick(point.name, point.type))
  })
})
</script>

<template>
  <div class="container mx-auto p-4 grid grid-cols-12 gap-4">
    <!-- Panel kiri -->
    <div class="col-span-4 bg-white rounded-lg shadow p-4">
      <div
        v-for="(item, index) in items"
        :key="index"
        class="flex items-center gap-4 mb-6 cursor-pointer hover:bg-gray-50 p-2 rounded-md transition"
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

    <!-- Peta kanan -->
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

.custom-marker-icon {
  background: none !important;
  border: none !important;
}
</style>
