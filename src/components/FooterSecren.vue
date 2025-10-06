<script setup lang="ts">
const scrollTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}
</script>

<!-- components/ModernFooter.vue -->
<template>
  <footer class="bg-gradient-to-r from-green-600 via-green-500 to-emerald-500 text-gray-100 mt-12 relative overflow-hidden">
    <div class="max-w-7xl mx-auto px-6 py-10 grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8">

      <!-- Column 1: Tentang -->
      <div>
        <h3 class="text-lg font-semibold mb-4">Tentang</h3>
        <p class="text-sm text-gray-100/90 mb-4">
          Platform POINT Tangerang Kota adalah …
          <!-- Deskripsi singkat tentang website/institusi -->
        </p>

        <!-- Button Login -->
        <button 
          class="bg-white text-green-700 font-semibold px-5 py-2 rounded-full shadow-md hover:bg-green-600 hover:text-white transition-all duration-300 transform hover:scale-105">
          Login
        </button>
      </div>

      <!-- Column 2: Layanan / Quick Links -->
      <div>
        <h3 class="text-lg font-semibold mb-4">Layanan</h3>
        <ul class="space-y-2 text-sm">
          <li><a href="#" class="hover:text-white transition-colors">Pelaporan</a></li>
          <li><a href="#" class="hover:text-white transition-colors">Peta Lokasi</a></li>
          <li><a href="#" class="hover:text-white transition-colors">FAQ</a></li>
          <li><a href="#" class="hover:text-white transition-colors">Bantuan</a></li>
        </ul>
      </div>

      <!-- Column 3: Kontak & Sosial Media -->
      <div>
        <h3 class="text-lg font-semibold mb-4">Kontak Kami</h3>
        <ul class="space-y-2 text-sm">
          <li class="flex items-center">
            <svg class="w-5 h-5 mr-2 fill-current"><!-- icon telepon --></svg>
            <span>+62 21 xxxx xxxx</span>
          </li>
          <li class="flex items-center">
            <svg class="w-5 h-5 mr-2 fill-current"><!-- icon email --></svg>
            <span>info@tangerangkota.go.id</span>
          </li>
          <li class="flex items-center">
            <svg class="w-5 h-5 mr-2 fill-current"><!-- icon alamat --></svg>
            <span>Alamat kantor</span>
          </li>
        </ul>
        <div class="flex space-x-4 mt-4">
          <a href="#" class="hover:text-white transition-colors"><svg class="w-6 h-6 fill-current"></svg></a>
          <a href="#" class="hover:text-white transition-colors"><svg class="w-6 h-6 fill-current"></svg></a>
          <a href="#" class="hover:text-white transition-colors"><svg class="w-6 h-6 fill-current"></svg></a>
        </div>
      </div>

      <!-- Column 4: Subscribe / Newsletter -->
      <div>
        <h3 class="text-lg font-semibold mb-4">Berlangganan</h3>
        <p class="text-sm mb-2 text-gray-100/90">Dapatkan update terbaru dari kami</p>
        <div class="flex">
          <input 
            type="email" 
            placeholder="Email Anda" 
            class="w-full px-3 py-2 rounded-l-md focus:outline-none text-gray-800" 
          />
          <button 
            class="px-4 py-2 bg-emerald-600 text-white rounded-r-md hover:bg-emerald-700 transition-colors">
            Subscribe
          </button>
        </div>
      </div>
    </div>

    <!-- Bottom bar -->
    <div class="border-t border-green-400/40 mt-8">
      <div class="max-w-7xl mx-auto px-6 py-4 flex flex-col sm:flex-row justify-between items-center text-sm">
        <div class="mb-2 sm:mb-0 text-gray-100/80">
          &copy; {{ new Date().getFullYear() }} Pemerintah Kota Tangerang. Semua Hak Dilindungi.
        </div>
        <div class="flex space-x-4">
          <a href="#" class="hover:text-white transition-colors">Kebijakan Privasi</a>
          <a href="#" class="hover:text-white transition-colors">Syarat & Ketentuan</a>
          <a href="#" class="hover:text-white transition-colors">Bantuan</a>
        </div>
      </div>
    </div>

    <!-- Back to Top Button -->
    <button 
      @click="scrollTop" 
      class="fixed bottom-5 right-5 bg-emerald-600 text-white p-3 rounded-full shadow-lg hover:bg-emerald-700 transition-all duration-300 hover:scale-110" 
      aria-label="Back to top">
      ↑
    </button>
  </footer>
</template>
