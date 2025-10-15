<script setup lang="ts"></script>

<template>
  <section
    class="relative min-h-screen bg-cover bg-center flex flex-col justify-center items-center text-white"
    style="background-image: url(&quot;/images/background_hero_1.jpg&quot;)"
  >
    <!-- Overlay -->
    <div
      class="absolute inset-0 bg-gradient-to-b from-black/40 to-black/60"
    ></div>

    <!-- Content -->
    <div class="relative z-10 text-center px-4">
      <h1 class="text-6xl font-bold tracking-wide animate-bounce-slow">
        POINT
      </h1>
     
      <p
        class="text-xl mt-3 font-medium bg-white/10 px-6 py-2 rounded-full inline-block"
      >
        Peta Potensi Dan Peluang Investasi - Kota Tangerang
      </p>

       <div class="mt-6 container w-full grid grid-cols-12 mx-auto bg-green-600 rounded-2xl p-6">
        <p class="col-span-12 text-white">
          POINT (Potential Opportunity and Investment) Kota Tangerang merupakan Mall Pusat Informasi
          Kota Tangerang berbasis platform WebGIS yang menyajikan informasi dan data strategis sektor
          unggulan, komoditas unggulan, peta potensi, serta peluang investasi, dilengkapi data daya
          dukung wilayah, baik di tingkat kabupaten/kota.
        </p>
      </div>

      <!-- Cards -->
      <!-- <div
        class="mt-10 grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-5 gap-6 max-w-6xl mx-auto"
      >
        <div class="bg-green-600 text-white p-6 rounded-xl shadow-lg">
          <h3 class="text-lg font-semibold mb-2">190.677 Unit</h3>
          <p class="text-sm">
            Jumlah Perusahaan Konstruksi<br /><span class="text-xs opacity-80"
              >(2023)</span
            >
          </p>
        </div>

        <div class="bg-green-600 text-white p-6 rounded-xl shadow-lg">
          <h3 class="text-lg font-semibold mb-2">9.92%</h3>
          <p class="text-sm">
            Kontribusi Sektor terhadap PDB<br /><span class="text-xs opacity-80"
              >(2023)</span
            >
          </p>
        </div>

        <div class="bg-green-600 text-white p-6 rounded-xl shadow-lg">
          <h3 class="text-lg font-semibold mb-2">2 Kuadriliun Rupiah</h3>
          <p class="text-sm">
            Nilai konstruksi yang diselesaikan<br /><span
              class="text-xs opacity-80"
              >(2023)</span
            >
          </p>
        </div>

        <div class="bg-green-600 text-white p-6 rounded-xl shadow-lg">
          <h3 class="text-lg font-semibold mb-2">30.964 orang</h3>
          <p class="text-sm">
            Tenaga Konstruksi Ahli<br /><span class="text-xs opacity-80"
              >(2023)</span
            >
          </p>
        </div>

        <div class="bg-green-600 text-white p-6 rounded-xl shadow-lg">
          <h3 class="text-lg font-semibold mb-2">74.217 orang</h3>
          <p class="text-sm">
            Tenaga Konstruksi Terampil<br /><span class="text-xs opacity-80"
              >(2023)</span
            >
          </p>
        </div>
      </div> -->

      <!-- External link (opens in new tab) -->
      <a
        href="https://point.tangerangkota.go.id/"
        target="_blank"
        rel="noopener noreferrer"
        class="mt-10 inline-block bg-white text-blue-700 font-semibold px-8 py-3 rounded-full shadow-lg hover:bg-blue-100 transition text-center"
        role="button"
      >
        KNOW MORE →
      </a>
    </div>
  </section>
</template>

<style scoped>
@keyframes bounce-slow {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

.animate-bounce-slow {
  animation: bounce-slow 3s ease-in-out infinite;
}

/* Animasi border berjalan */
@keyframes border-move {
  0% {
    border-color: rgba(255, 255, 255, 0.7);
  }
  50% {
    border-color: rgba(255, 255, 255, 0.3);
  }
  100% {
    border-color: rgba(255, 255, 255, 0.7);
  }
}

.animate-border-move {
  animation: border-move 4s linear infinite;
}
</style>
