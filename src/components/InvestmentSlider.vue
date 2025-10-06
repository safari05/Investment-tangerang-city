<template>
  <div class="max-w-5xl mx-auto p-4">

    <!-- Carousel Kartu -->
    <Carousel
      :itemsToShow="5"
      :wrapAround="true"
      :mouseDrag="true"
      :snapAlign="'center'"
      :autoplayTimeout="8000"  
      :transition="300"
      :showArrows="true"
      class="mb-6"
    >
      <Slide v-for="(card, i) in cards" :key="card.title">
        <div
          @click="selectCard(i)"
          :class="[
            'flex flex-col items-center justify-center cursor-pointer rounded-lg shadow px-4 py-3',
            card.active ? 'bg-orange-500 text-white' : 'bg-blue-800 text-white',
            'transition-colors duration-300'
          ]"
          style="min-width: 140px; height: 96px"
        >
          <i :class="card.icon" class="text-2xl mb-1"></i>
          <span class="text-sm font-semibold">{{ card.title }}</span>
        </div>
      </Slide>
    </Carousel>

    <!-- Konten yang berubah sesuai kartu -->
    <div class="border rounded-lg p-6 shadow-lg">
      <img
        :src="selectedCard.image"
        alt="image"
        class="rounded-lg w-full h-40 object-cover mb-4"
      />
      <h2 class="font-bold text-xl mb-2">{{ selectedCard.title }}</h2>
      <p class="text-sm text-gray-700">{{ selectedCard.description }}</p>
    </div>

  </div>
</template>

<script lang="ts" setup>
import { ref, computed } from 'vue'
import { Carousel, Slide } from 'vue3-carousel'
import 'vue3-carousel/dist/carousel.css'

interface CardItem {
  title: string
  icon: string
  active: boolean
  image: string
  description: string
}

// Data kartu
const cards = ref<CardItem[]>([
  {
    title: 'PERIKANAN',
    icon: 'fas fa-fish',
    active: false,
    image: '/images/perikanan.webp',
    description: 'Deskripsi singkat sektor perikanan.'
  },
  {
    title: 'PERINDUSTRIAN',
    icon: 'fas fa-industry',
    active: true,
    image: '/images/perindustrian.webp',
    description:
      'Pada tahun 2023, Indonesia berkontribusi sebesar 1,4 persen terhadap produk manufaktur global dengan sektor industri pengolahan menjadi penyumbang terbesar...'
  },
  {
    title: 'PERTANIAN',
    icon: 'fas fa-seedling',
    active: false,
    image: '/images/pertanian.jpg',
    description: 'Deskripsi singkat sektor pertanian.'
  },
  {
    title: 'PARIWISATA',
    icon: 'fas fa-umbrella-beach',
    active: false,
    image: '/images/pariwisata.jpg',
    description: 'Deskripsi singkat sektor pariwisata.'
  },
  {
    title: 'KONSTRUKSI',
    icon: 'fas fa-tools',
    active: false,
    image: '/images/kontruksi.jpg',
    description: 'Deskripsi singkat sektor konstruksi.'
  }
])

// Index kartu aktif
const activeIndex = ref(1)

// Fungsi pilih kartu dan update active status
function selectCard(index: number) {
  activeIndex.value = index
  cards.value.forEach((c, i) => (c.active = i === index))
}

// computed untuk kartu aktif
const selectedCard = computed(() => cards.value[activeIndex.value])
</script>

<style scoped>
@import 'https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css';
</style>
