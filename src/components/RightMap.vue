<script setup lang="ts">
import { onMounted, watch, ref } from 'vue'
import L from 'leaflet'
import 'leaflet/dist/leaflet.css'

// patch typing conflict
declare module 'leaflet' {
  export interface Map {}
  export interface LayerGroup {}
}

const props = defineProps<{
  markers: { lat: number; lng: number; title: string }[]
}>()

const map = ref<InstanceType<typeof L.Map> | null>(null)
const markerGroup = ref<InstanceType<typeof L.LayerGroup> | null>(null)

// simple circular div icon (inline styles so no external assets needed)
const customIcon = L.divIcon({
  html: `
    <span style="background:#1e40af;border:2px solid #ffffff;border-radius:50%;width:20px;height:20px;display:block;box-shadow:0 2px 6px rgba(0,0,0,0.3);"></span>
  `,
  className: '',
  iconSize: [20, 20],
  iconAnchor: [10, 10],
})

onMounted(() => {
  map.value = L.map('map').setView([-6.1783, 106.6319], 12)

  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    maxZoom: 18,
    attribution: '© OpenStreetMap contributors',
  }).addTo(map.value)

  markerGroup.value = L.layerGroup().addTo(map.value)
})

watch(
  () => props.markers,
  (newMarkers) => {
    if (!map.value || !markerGroup.value) return

    markerGroup.value.clearLayers()
    if (!newMarkers.length) return

    const leafletMarkers = newMarkers.map((m) =>
      L.marker([m.lat, m.lng], { icon: customIcon }).bindPopup(m.title)
    )

    leafletMarkers.forEach((m) => m.addTo(markerGroup.value!))

    const group = L.featureGroup(leafletMarkers)
    map.value.fitBounds(group.getBounds(), { padding: [40, 40] })
  },
  { deep: true }
)
</script>

<template>
  <div id="map" class="w-full h-[80vh] rounded-2xl shadow-md"></div>
</template>
