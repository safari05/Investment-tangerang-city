<script setup lang="ts">
import { HandCoins, FlaskRound, Building2, Wallet, ShoppingBag, Pickaxe, Sprout } from 'lucide-vue-next'

const sectors = [
  { title: 'Industri Barang Konsumsi', icon: HandCoins, bg: 'bg-blue-700', textColor: 'text-blue-700' },
  { title: 'Industri Dasar dan Kimia', icon: FlaskRound, bg: 'bg-green-700', textColor: 'text-green-700' },
  { title: 'Infrastruktur, Utilitas, dan Transportasi', icon: Building2, bg: 'bg-yellow-500', textColor: 'text-yellow-500' },
  { title: 'Keuangan', icon: Wallet, bg: 'bg-blue-600', textColor: 'text-blue-600' },
  { title: 'Perdagangan, Jasa dan Investasi', icon: ShoppingBag, bg: 'bg-red-600', textColor: 'text-red-600' },
  { title: 'Pertambangan', icon: Pickaxe, bg: 'bg-orange-500', textColor: 'text-orange-500' },
  { title: 'Pertanian', icon: Sprout, bg: 'bg-green-800', textColor: 'text-green-800' },
  // bisa tambahkan item baru bila diperlukan
]
</script>

<!-- components/InvestmentOpportunities.vue -->
<template>
  <section class="bg-white py-16">
    <div class="max-w-7xl mx-auto px-6 text-center">
      <!-- Judul -->
      <h2 class="text-2xl sm:text-3xl font-bold text-green-700 mb-2">
        Peluang Investasi
      </h2>
      <div class="h-1 w-16 bg-green-500 mx-auto mb-10 rounded-full"></div>

      <!-- Grid sektor -->
      <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-4 lg:grid-cols-7 gap-8">
        <div v-for="(item, index) in sectors" :key="index" class="flex flex-col items-center">
          <div :class="`w-16 h-16 rounded-full flex items-center justify-center text-white text-2xl shadow-lg ${item.bg}`">
            <component :is="item.icon" />
          </div>
          <p class="mt-4 text-sm font-semibold text-gray-800">{{ item.title }}</p>
          <p :class="`font-semibold mt-1 ${item.textColor}`">180 Sektor</p>
        </div>
      </div>
    </div>
  </section>
</template>



<style scoped>
/* animasi hover halus */
div:hover > .rounded-full {
  transform: scale(1.05);
  transition: transform 0.3s ease;
}
</style>
