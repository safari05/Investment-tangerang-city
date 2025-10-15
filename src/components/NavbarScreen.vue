<script setup lang="ts">
import { ref } from "vue";

const toggleMobile = ref(false);
</script>


<!-- components/Navbar.vue -->
<template>
  <nav class="bg-white shadow-md fixed top-0 left-0 w-full z-20">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between items-center h-16">
        <!-- Logo / Brand -->
        <div class="flex-shrink-0">
          <router-link to="/">           
            <!-- Atau teks saja -->
           <span
            class="text-2xl font-extrabold bg-gradient-to-r from-green-600 via-emerald-500 to-lime-400 text-transparent bg-clip-text
                  transition-all duration-500 hover:scale-105 hover:from-lime-400 hover:to-green-700 cursor-pointer"
          >
            POINT Tangerang
          </span>

          </router-link>
        </div>

        <!-- Menu links (desktop) -->
        <div class="hidden md:flex space-x-6">
          <router-link to="/" class="text-gray-700 hover:text-green-700 transition">Beranda</router-link>
          <router-link to="/komoditi" class="text-gray-700 hover:text-green-700 transition">Sektor Unggulan</router-link>
        </div>
        <!-- Hamburger mobile -->
        <div class="md:hidden">
          <button @click="toggleMobile = !toggleMobile" class="text-gray-700 hover:text-green-700 focus:outline-none">
            <svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path
                v-if="!toggleMobile"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M4 6h16M4 12h16M4 18h16"
              />
              <path
                v-if="toggleMobile"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M6 18L18 6M6 6l12 12"
              />
            </svg>
          </button>
        </div>
      </div>
    </div>

    <!-- Menu mobile -->
    <div v-if="toggleMobile" class="md:hidden bg-white shadow-md">
      <router-link
        to="/"
        class="block px-4 py-2 text-gray-700 hover:bg-green-50 hover:text-green-700 transition"
        @click="toggleMobile = false"
      >
        Beranda
      </router-link>
      <router-link
        to="/komoditi"
        class="block px-4 py-2 text-gray-700 hover:bg-green-50 hover:text-green-700 transition"
        @click="toggleMobile = false"
      >
        Komoditi
      </router-link>
      <router-link
        to="/peta"
        class="block px-4 py-2 text-gray-700 hover:bg-green-50 hover:text-green-700 transition"
        @click="toggleMobile = false"
      >
        Peta
      </router-link>
      <router-link
        to="/tentang"
        class="block px-4 py-2 text-gray-700 hover:bg-green-50 hover:text-green-700 transition"
        @click="toggleMobile = false"
      >
        Tentang
      </router-link>
      <router-link
        to="/login"
        class="block px-4 py-2 text-white bg-green-600 hover:bg-green-700 transition mt-2 mx-4 rounded-lg text-center"
        @click="toggleMobile = false"
      >
        Login
      </router-link>
    </div>
  </nav>
</template>


<style scoped>
/* tambahkan top padding di body agar konten tidak tertutup navbar */
body {
  padding-top: 4rem; /* disesuaikan tinggi navbar */
}
</style>
