<script setup lang="ts">
import FooterSecren from '../components/FooterSecren.vue';
import LeftKomoditi from '../components/LeftKomoditi.vue';
import NavbarScreen from '../components/NavbarScreen.vue';
import RightMap from '../components/RightMap.vue';

const daftarKomoditas = [
  {
    nama: "Kopi Arabika",
    kategori: "Pertanian",
    lokasi: "Cisoka",
    keterangan: "Potensi ekspor tinggi",
  },
  {
    nama: "Industri Tekstil",
    kategori: "Industri",
    lokasi: "Jatiuwung",
    keterangan: "Memiliki fasilitas lengkap",
  },
  {
    nama: "Buah Naga Merah",
    kategori: "Holtikultura",
    lokasi: "Ciledug",
    keterangan: "Produksi berkelanjutan",
  },
];
</script>

<template>
   <NavbarScreen />
    <section class="relative min-h-screen overflow-hidden pt-20">
    <!-- 🌈 Animated Gradient Background -->
    <div
      class="absolute inset-0 bg-gradient-to-br from-green-100 via-white to-green-50 animate-gradient-slow pt-20"
    ></div>

    <!-- ✨ Overlay pattern dots -->
    <div
      class="absolute inset-0 opacity-30 bg-[radial-gradient(circle_at_1px_1px,_rgba(0,0,0,0.05)_1px,_transparent_0)] [background-size:20px_20px]"
    ></div>

    <!-- 🧩 Main Content -->
    <div
      class="relative z-10 max-w-7xl mx-auto px-4 py-12 grid grid-cols-1 sm:grid-cols-3 gap-4 sm:gap-6"
    >
      <LeftKomoditi class="sm:col-span-1 transition-transform duration-500 hover:-translate-y-1" />
      <RightMap class="sm:col-span-2 transition-transform duration-500 hover:-translate-y-1" />
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
              class="hover:bg-green-50/60 transition-colors duration-300"
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
    </div>
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
