<script setup lang="ts">
import { ref } from 'vue';
import FooterSecren from '../components/FooterSecren.vue';
import LeftKomoditi from '../components/LeftKomoditi.vue';
import NavbarScreen from '../components/NavbarScreen.vue';
import RightMap from '../components/RightMap.vue';
import SampleChart from '../components/SampleChart.vue';

const daftarKomoditas = [
  {
    nama: "Padi",
    kategori: "Pertanian",
    lokasi: "Cisoka",
    keterangan: "Potensi ekspor tinggi",
    image: "/images/pertanian.jpg",
    informasi: {
      luasPanen: "1.04 Juta Hektar (2021)",
      produktivitas: "5.14 Ton/Hektar (2021)",
      totalProduksi: "53.55 Juta Ton (2021)",
      konsumsi: "94.38 Ribu Kg/Kapita (2021)",
      luasTanam: "11.07 Juta Hektar (2021)",
      sentra: "Kota Tangerang",
      produksi: "Kota Tangerang | Cisoka",
    },
  },
  {
    nama: "Bayam",
    kategori: "Pertanian",
    lokasi: "Jatiuwung",
    keterangan: "Memiliki fasilitas lengkap",
    image: "/images/pertanian.jpg",
    informasi: {
      luasPanen: "68.24 Juta Hektar (2021)",
      produktivitas: "2.02 Ton/Hektar (2021)",
      totalProduksi: "53.55 Juta Ton (2021)",
      konsumsi: "37.0 Ribu Kg/Kapita (2021)",
      luasTanam: "68.24 Juta Hektar (2021)",
      sentra: "Kota Tangerang",
      produksi: "Kota Tangerang | Jatiuwung",
    },
  },
  {
    nama: "Buah Naga Merah",
    kategori: "Holtikultura",
    lokasi: "Ciledug",
    keterangan: "Produksi berkelanjutan",
    image: "/images/pertanian.jpg",
  },
];

interface Marker {
  lat: number;
  lng: number;
  title: string;
}

const selectedMarkers = ref<Marker[]>([]);

const handleShowMarkers = (markers: Marker[]) => {
  selectedMarkers.value = markers;
};

// Modal state for showing komoditas details
const showModal = ref(false)
const activeItem = ref<{
  nama: string
  kategori: string
  lokasi: string
  keterangan: string
  image?: string
  informasi?: {
    luasPanen?: string
    produktivitas?: string
    totalProduksi?: string
    konsumsi?: string
    luasTanam?: string
    sentra?: string
    produksi?: string
  }
} | null>(null)

const openModal = (item: { nama: string; kategori: string; lokasi: string; keterangan: string; image?: string; informasi?: any }) => {
  activeItem.value = item
  showModal.value = true
}

const closeModal = () => {
  showModal.value = false
  activeItem.value = null
}

</script>

<template>
   <NavbarScreen />
    <section class="relative min-h-screen overflow-hidden pt-20">
    <div
      class="absolute inset-0 bg-gradient-to-br from-green-100 via-white to-green-50 animate-gradient-slow pt-20"
    ></div>
    <div
      class="absolute inset-0 opacity-30 bg-[radial-gradient(circle_at_1px_1px,_rgba(0,0,0,0.05)_1px,_transparent_0)] [background-size:20px_20px]"
    ></div>
    <div
      class="relative z-10 max-w-7xl mx-auto px-4 py-12 grid grid-cols-1 sm:grid-cols-3 gap-4 sm:gap-6"
    >
      <LeftKomoditi class="sm:col-span-1 transition-transform duration-500 hover:-translate-y-1" @showMarkers="handleShowMarkers" />
      <RightMap :markers="selectedMarkers" class="sm:col-span-2 transition-transform duration-500 hover:-translate-y-1" />
      
    </div>

    <!-- 📊 Tabel Daftar Komoditas -->
    <div class="relative z-10 max-w-7xl mx-auto px-4 mt-10">
      <h2
        class="text-2xl font-semibold mb-5 text-gray-700 border-l-4 border-green-500 pl-3 tracking-wide"
      >
        Daftar Komoditas
      </h2>

      <div
        class="overflow-x-auto bg-white/90 backdrop-blur-md shadow-xl rounded-2xl border border-green-100 animate-fade-in"
      >
        <table class="min-w-full divide-y divide-gray-200 text-sm">
          <thead class="bg-green-600 text-white">
            <tr>
              <th
                class="px-6 py-3 text-left font-medium uppercase tracking-wider"
              >
                No
              </th>
              <th
                class="px-6 py-3 text-left font-medium uppercase tracking-wider"
              >
                Nama Komoditas
              </th>
              <th
                class="px-6 py-3 text-left font-medium uppercase tracking-wider"
              >
                Kategori
              </th>
              <th
                class="px-6 py-3 text-left font-medium uppercase tracking-wider"
              >
                Lokasi
              </th>
              <th
                class="px-6 py-3 text-left font-medium uppercase tracking-wider"
              >
                Keterangan
              </th>
            </tr>
          </thead>
          <tbody class="divide-y divide-gray-100">
            <tr
              v-for="(item, index) in daftarKomoditas"
              :key="index"
              class="hover:bg-green-50/60 transition-colors duration-300 cursor-pointer"
              @click="openModal(item)"
            >
              <td class="px-6 py-3 font-medium text-gray-700">
                {{ index + 1 }}
              </td>
              <td class="px-6 py-3">{{ item.nama }}</td>
              <td class="px-6 py-3">{{ item.kategori }}</td>
              <td class="px-6 py-3">{{ item.lokasi }}</td>
              <td class="px-6 py-3 text-gray-600">
                {{ item.keterangan }}
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      <SampleChart class="mt-10"/>
    </div>
    
    <!-- Modal -->
    <transition name="fade">
  <div
    v-if="showModal"
    class="fixed inset-0 z-50 flex items-center justify-center px-4"
  >
    <div class="absolute inset-0 bg-black/50" @click="closeModal"></div>

    <div class="relative z-10 w-full max-w-5xl bg-white rounded-2xl shadow-xl overflow-y-auto max-h-[90vh]">
      <div class="w-full h-64 sm:h-80 bg-gray-100">
        <img
          :src="activeItem?.image || '/images/background_hero_1.jpg'"
          alt="Image"
          class="w-full h-full object-cover"
        />
      </div>

      <div class="p-6">
        <div class="flex items-start justify-between">
          <h3 class="text-2xl font-semibold text-gray-800">{{ activeItem?.nama }}</h3>
          <button class="text-gray-400 hover:text-gray-600 text-xl" @click="closeModal">✕</button>
        </div>

        <div class="mt-4 text-base text-gray-700">
          <p class="mb-2"><strong>Kategori:</strong> {{ activeItem?.kategori }}</p>
          <p class="mb-2"><strong>Lokasi:</strong> {{ activeItem?.lokasi }}</p>
          <p class="mb-2"><strong>Keterangan:</strong> {{ activeItem?.keterangan }}</p>
        </div>


<!-- Informasi Detail -->
<div v-if="activeItem?.informasi" class="mt-6 border-t pt-6">
  <h4 class="text-lg font-semibold mb-4 text-green-700">Informasi Detail</h4>

  <!-- dua kolom di layar besar -->
  <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
    <ul class="space-y-1">
      <li><strong>Luas Panen:</strong> {{ activeItem.informasi.luasPanen }}</li>
      <li><strong>Produktivitas:</strong> {{ activeItem.informasi.produktivitas }}</li>
      <li><strong>Total Produksi:</strong> {{ activeItem.informasi.totalProduksi }}</li>
      <li><strong>Konsumsi:</strong> {{ activeItem.informasi.konsumsi }}</li>
    </ul>
    <ul class="space-y-1">
      <li><strong>Luas Tanam:</strong> {{ activeItem.informasi.luasTanam }}</li>
      <li><strong>Sentra:</strong> {{ activeItem.informasi.sentra }}</li>
      <li><strong>Produksi:</strong> {{ activeItem.informasi.produksi }}</li>
    </ul>
  </div>
</div>

<!-- 🎯 Chart khusus Bayam -->
<div
  v-if="activeItem?.nama === 'Bayam'"
  class="mt-8 border-t pt-6"
>
  <h4 class="text-lg font-semibold text-green-700 mb-3">
    Grafik Produksi Bayam
  </h4>
  <SampleChart class="max-w-3xl mx-auto" />
</div>


        <div class="mt-6 flex justify-end">
          <button
            class="bg-green-600 text-white px-5 py-2 rounded-lg shadow hover:bg-green-700"
            @click="closeModal"
          >
            Tutup
          </button>
        </div>
      </div>
    </div>
  </div>
</transition>

    
  </section>
  
  <FooterSecren/>
</template>


<style scoped>
@keyframes gradient-slow {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

.animate-gradient-slow {
  background-size: 200% 200%;
  animation: gradient-slow 12s ease infinite;
}

@keyframes fade-in {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-fade-in {
  animation: fade-in 1s ease-in-out forwards;
}
</style>