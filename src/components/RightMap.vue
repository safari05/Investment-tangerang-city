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
      L.marker([m.lat, m.lng]).bindPopup(m.title)
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
