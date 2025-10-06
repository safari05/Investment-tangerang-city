

<script setup lang="ts">
import { onMounted } from 'vue'
import L from 'leaflet'
import 'leaflet/dist/leaflet.css'

onMounted(() => {
  const map = L.map('map').setView([-6.1783, 106.6319], 12)

  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    maxZoom: 18,
    attribution: '© OpenStreetMap contributors'
  }).addTo(map)

  // contoh marker
  L.marker([-6.1783, 106.6319]).addTo(map).bindPopup("Kota Tangerang")
})
</script>

<!-- components/LeafletMap.vue -->
<template>
  <div id="map" class="w-full h-[80vh] rounded-2xl shadow-md"></div>
</template>

