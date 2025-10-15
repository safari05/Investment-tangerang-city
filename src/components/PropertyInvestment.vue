<template>
  <section class="px-8 py-6 bg-gray-50">
    <div class="flex items-center justify-between mb-4">
      <h2 class="text-2xl font-semibold text-gray-800">Daftar Properti</h2>

      <!-- Tombol Navigasi -->
      <div class="flex gap-2">
        <button ref="prevEl" class="swiper-nav-btn bg-white p-2 rounded-full shadow hover:bg-gray-100">
          ◀
        </button>
        <button ref="nextEl" class="swiper-nav-btn bg-white p-2 rounded-full shadow hover:bg-gray-100">
          ▶
        </button>
      </div>
    </div>

    <!-- Swiper Slider -->
   <div class="container mx-auto">
 <Swiper
      :modules="[Navigation, Pagination, Autoplay]"
      :slides-per-view="3"
      :space-between="20"
      :loop="true"
      :navigation="{ prevEl: prevEl, nextEl: nextEl }"
      :pagination="{ clickable: true }"
      :autoplay="{ delay: 3000, disableOnInteraction: false }"
      :breakpoints="{
        320: { slidesPerView: 1 },
        768: { slidesPerView: 2 },
        1024: { slidesPerView: 3 }
      }"
      class="property-swiper"
    >
      <SwiperSlide v-for="(item, index) in properties" :key="index">
        <div
          class="bg-green-200 container rounded-xl shadow-md overflow-hidden hover:shadow-lg transition-all duration-300"
        >
          <img
            :src="item.image"
            alt="Property Image"
            class="w-full h-48 object-cover"
          />
          <div class="p-4">
            <div class="flex justify-between items-center mb-2">
              <span class="text-xs px-2 py-1 bg-purple-600 text-white rounded-md uppercase">
                {{ item.category }}
              </span>
              <span
                class="text-xs font-semibold px-2 py-1 rounded-md uppercase"
                :class="item.tag === 'POTENSI' ? 'bg-yellow-400 text-black' : 'bg-green-500 text-white'"
              >
                {{ item.tag }}
              </span>
            </div>
            <h3 class="font-semibold text-gray-800 text-lg mb-1">
              {{ item.title }}
            </h3>
            <p class="text-sm text-gray-500 mb-2">{{ item.location }}</p>
            <div class="flex items-center text-xs text-gray-400">
              <span class="mr-3">🏙️ {{ item.city }}</span>
              <span>📅 {{ item.year }}</span>
            </div>
          </div>
        </div>
      </SwiperSlide>
    </Swiper>
   </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { Swiper, SwiperSlide } from "swiper/vue";
import { Navigation, Pagination, Autoplay } from "swiper/modules";
import "swiper/css";
import "swiper/css/navigation";
import "swiper/css/pagination";

interface Property {
  title: string;
  image: string;
  category: string;
  tag: string;
  location: string;
  city: string;
  year: number;
}

// Refs untuk tombol navigasi Swiper
const prevEl = ref<HTMLElement | null>(null);
const nextEl = ref<HTMLElement | null>(null);

// Data properti (dummy)
const properties: Property[] = [
  {
    title: "ICONIC OFFICE TOWER",
    image: "/images/Cover Iconic.PNG",
    category: "PROPERTI",
    tag: "PELUANG",
    location: "Kelurahan Panunggangan Utara, Pinang",
    city: "Tangerang",
    year: 2025,
  },
  {
    title: "DUTA INDAH STARHUB",
    image: "/images/Duta_Indah_Starhub.PNG",
    category: "PROPERTI",
    tag: "PELUANG",
    location: "Kelurahan Belendung, Benda",
    city: "Tangerang",
    year: 2025,
  },
  {
    title: "GRAHA RAYA",
    image: "/images/graha_cahaya.jpg",
    category: "PROPERTI",
    tag: "POTENSI",
    location: "Kelurahan Sudimara Pinang, Pinang",
    city: "Tangerang",
    year: 2025,
  },
  {
    title: "PERUMAHAN ALAM SUTERA",
    image: "/images/alamSutra.jpg",
    category: "PROPERTI",
    tag: "POTENSI",
    location: "Kelurahan Kunciran, Pinang",
    city: "Tangerang",
    year: 2021,
  },
  {
    title: "CISADANE WALK",
    image: "/images/cisadane.jpeg",
    category: "PARIWISATA",
    tag: "POTENSI",
    location: "Kelurahan Sukarasa, Tangerang",
    city: "Tangerang",
    year: 2021,
  },
];
</script>

<style scoped>
.property-swiper {
  padding-bottom: 2rem;
}

.swiper-pagination-bullet {
  background-color: #a855f7; /* warna ungu */
}

.swiper-pagination-bullet-active {
  background-color: #7e22ce;
}
</style>
