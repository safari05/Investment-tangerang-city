<template>
  <aside class="w-full sm:w-80 bg-white shadow-lg rounded-2xl p-4 sm:p-6 overflow-y-auto">
    <h2 class="text-xl font-semibold text-green-700 mb-4">Cari Komoditi</h2>

    <div
      v-for="kategori in kategoriList"
      :key="kategori.nama"
      class="mb-4 border rounded-lg overflow-hidden"
    >
      <!-- Tombol kategori utama -->
      <button
        class="flex items-center justify-between w-full px-4 py-2 bg-green-50 hover:bg-green-100 transition"
        @click="kategori.expanded = !kategori.expanded"
      >
        <div class="flex items-center space-x-2">
          <img :src="kategori.icon" class="w-6 h-6" />
          <span class="font-medium text-gray-800">{{ kategori.nama }}</span>
        </div>
        <span class="text-lg">{{ kategori.expanded ? '−' : '+' }}</span>
      </button>

      <!-- Isi kategori (expand) -->
      <div v-if="kategori.expanded" class="px-4 py-2 bg-white text-sm text-gray-700">
        <ul class="space-y-1">
          <li
            v-for="sub in kategori.sub"
            :key="sub.nama"
            class="border-b border-gray-100 pb-1"
          >
            <div class="flex justify-between items-center">
              <span
                class="cursor-pointer hover:text-green-600 transition font-medium"
                @click="sub.submenu ? (sub.expanded = !sub.expanded) : null"
              >
                {{ sub.nama }}
              </span>
              <span
                v-if="sub.submenu"
                class="text-gray-500 text-sm cursor-pointer"
                @click="sub.expanded = !sub.expanded"
              >
                {{ sub.expanded ? '−' : '+' }}
              </span>
            </div>

            <!-- Submenu jika ada -->
            <ul v-if="sub.submenu && sub.expanded" class="pl-4 mt-1 text-gray-600">
              <li
                v-for="item in sub.submenu"
                :key="item"
                class="hover:text-green-500 cursor-pointer transition"
              >
                • {{ item }}
              </li>
            </ul>
          </li>
        </ul>
      </div>
    </div>
  </aside>
</template>

<script setup lang="ts">
import { ref } from "vue";

const kategoriList = ref([
  {
    nama: "Perdagangan",
    icon: "https://cdn-icons-png.flaticon.com/512/2331/2331943.png",
    expanded: false,
    sub: [
      {
        nama: "Unggulan",
        expanded: false,
        submenu: ["Pasar Modern", "Pasar Tradisional", "Distribusi Barang"],
      },
      {
        nama: "Non-Unggulan",
        expanded: false,
        submenu: ["Toko Grosir", "Retail Kecil"],
      },
    ],
  },
  {
    nama: "Industri",
    icon: "https://cdn-icons-png.flaticon.com/512/3208/3208679.png",
    expanded: false,
    sub: [
      {
        nama: "Jenis Industri",
        expanded: false,
        submenu: ["Pabrik Makanan", "Pabrik Tekstil", "Pabrik Logam"],
      },
    ],
  },
  {
    nama: "Holtikultura",
    icon: "https://cdn-icons-png.flaticon.com/512/4150/4150930.png",
    expanded: false,
    sub: [
      {
        nama: "Jenis Tanaman",
        expanded: false,
        submenu: ["Sayur", "Buah", "Tanaman Hias"],
      },
    ],
  },
  {
    nama: "Biofarmaka",
    icon: "https://cdn-icons-png.flaticon.com/512/765/765477.png",
    expanded: false,
    sub: [
      {
        nama: "Jenis Tanaman Obat",
        expanded: false,
        submenu: ["Jahe", "Kunyit", "Temulawak"],
      },
    ],
  },
]);
</script>

<style scoped>
aside::-webkit-scrollbar {
  width: 6px;
}
aside::-webkit-scrollbar-thumb {
  background-color: #a7f3d0;
  border-radius: 6px;
}
</style>
