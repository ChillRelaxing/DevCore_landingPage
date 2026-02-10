<script setup lang="ts">
const stats = [
  { label: 'Proyectos Finalizados', value: '250+', icon: 'M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z' },
  { label: 'Clientes Globales', value: '120+', icon: 'M3.055 11H5a2 2 0 012 2v1a2 2 0 002 2 2 2 0 012 2v2.945M8 3.935V5.5A2.5 2.5 0 0010.5 8h.5a2 2 0 012 2 2 2 0 104 0 2 2 0 012-2h1.064M15 20.488V18a2 2 0 012-2h3.064M21 12a9 9 0 11-18 0 9 9 0 0118 0z' },
  { label: 'Tasa de Éxito', value: '98%', icon: 'M13 7h8m0 0v8m0-8l-8 8-4-4-6 6' },
  { label: 'Años de Innovación', value: '10+', icon: 'M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z' },
]
</script>

<template>
  <section id="estadisticas" class="py-20 bg-indigo-600 dark:bg-indigo-900/20">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="grid grid-cols-2 lg:grid-cols-4 gap-8 md:gap-12">
        <div v-for="stat in stats" :key="stat.label" class="text-center group">
          <div class="inline-flex items-center justify-center w-12 h-12 mb-4 rounded-xl bg-white/10 text-white group-hover:scale-110 transition-transform">
            <svg class="w-6 h-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" :d="stat.icon" />
            </svg>
          </div>
          <div class="text-3xl md:text-5xl font-black text-white mb-2">{{ stat.value }}</div>
          <div class="text-indigo-100 dark:text-indigo-300 font-medium uppercase tracking-wider text-xs md:text-sm">{{ stat.label }}</div>
        </div>
      </div>
    </div>
  </section>
</template>
