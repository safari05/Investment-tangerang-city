<script setup lang="ts">
import { ref } from "vue";

const emit = defineEmits(["showMarkers"]);

const kategoriList = ref([
  {
    nama: "Pertanian",
    icon: "https://cdn-icons-png.flaticon.com/512/2331/2331943.png",
    expanded: false,
    children: [
      {
        nama: "Hortikultura",
        expanded: false,
        children: [
          {
            nama: "Bayam",
            markers: [
              { lat: -6.17, lng: 106.63, title: "Bayam 1" },
              { lat: -6.20, lng: 106.64, title: "Bayam 2" },
            ],
          },
          {
            nama: "Kangkung",
            markers: [
              { lat: -6.18, lng: 106.61, title: "Kangkung 1" },
              { lat: -6.19, lng: 106.65, title: "Kangkung 2" },
            ],
          },
          {
            nama: "Melinjo",
            markers: [
              { lat: -6.22, lng: 106.66, title: "Gudang Utama" },
              { lat: -6.23, lng: 106.62, title: "Pusat Logistik" },
            ],
          },
        ],
      },
      {
        nama: "Biofarmaka",
        expanded: false,
        children: [
          {
            nama: "Mini Market",
            markers: [
              { lat: -6.25, lng: 106.67, title: "Alfamart Ciledug" },
              { lat: -6.26, lng: 106.68, title: "Indomaret Pinang" },
            ],
          },
        ],
      },
    ],
  },
  {
    nama: "Industri",
    icon: "https://cdn-icons-png.flaticon.com/512/3208/3208679.png",
    expanded: false,
  },
  {
    nama: "Holtikultura",
    icon: "https://cdn-icons-png.flaticon.com/512/4150/4150930.png",
    expanded: false,
  },
  {
    nama: "Biofarmaka",
    icon: "https://cdn-icons-png.flaticon.com/512/765/765477.png",
    expanded: false,
  },
]);

// Toggle kategori utama
const toggleKategori = (kategori: any) => {
  kategori.expanded = !kategori.expanded;
};

// Toggle subkategori (Unggulan / Non-Unggulan)
const toggleSubKategori = (sub: any) => {
  sub.expanded = !sub.expanded;
};

// Klik subchild (menampilkan sebaran marker)
const showMarkers = (markers: any[]) => {
  emit("showMarkers", markers);
};
</script>

<template>
  <aside
    class="w-full sm:w-80 bg-white shadow-lg rounded-2xl p-4 sm:p-6 overflow-y-auto"
  >
    <h2 class="text-xl font-semibold text-green-700 mb-4">Cari Komoditi</h2>

    <div
      v-for="kategori in kategoriList"
      :key="kategori.nama"
      class="mb-4 border rounded-lg overflow-hidden"
    >
      <!-- KATEGORI UTAMA -->
      <button
        class="flex items-center justify-between w-full px-4 py-2 bg-green-50 hover:bg-green-100 transition"
        @click="toggleKategori(kategori)"
      >
        <div class="flex items-center space-x-2">
          <img :src="kategori.icon" class="w-6 h-6" />
          <span class="font-medium text-gray-800">{{ kategori.nama }}</span>
        </div>
        <span class="text-lg">{{ kategori.expanded ? "−" : "+" }}</span>
      </button>

      <!-- SUBMENU LEVEL 1 -->
      <transition name="fade">
        <div
          v-if="kategori.expanded && kategori.children"
          class="bg-gray-50 border-t px-4 py-2 space-y-2"
        >
          <div
            v-for="sub in kategori.children"
            :key="sub.nama"
            class="border rounded-md bg-white"
          >
            <button
              class="w-full text-left px-3 py-2 font-medium text-green-700 border-b hover:bg-green-50 flex justify-between"
              @click="toggleSubKategori(sub)"
            >
              <span>{{ sub.nama }}</span>
              <span class="text-sm">{{ sub.expanded ? "−" : "+" }}</span>
            </button>

            <!-- SUBMENU LEVEL 2 -->
            <transition name="fade">
              <ul
                v-if="sub.expanded && sub.children"
                class="pl-6 py-2 text-sm text-gray-700 space-y-1"
              >
                <li
                  v-for="child in sub.children"
                  :key="child.nama"
                  class="cursor-pointer hover:text-green-600 flex items-center space-x-1"
                  @click="showMarkers(child.markers)"
                >
                  <span>•</span>
                  <span>{{ child.nama }}</span>
                </li>
              </ul>
            </transition>
          </div>
        </div>
      </transition>
    </div>
  </aside>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: all 0.3s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(-5px);
}
</style>
