<script setup lang="ts">
interface Testimonial {
  name: string;
  role: string;
  comment: string;
  rating: number;
  image: string;
}

const testimonials: Testimonial[] = [
  {
    name: 'Ana García',
    role: 'CEO de Nexus Bank',
    comment: 'DevCore superó todas nuestras expectativas. Su capacidad técnica es inigualable y entendieron perfectamente nuestra visión desde el primer día.',
    rating: 5,
    image: 'https://images.unsplash.com/photo-1494790108377-be9c29b29330?auto=format&fit=crop&q=80&w=150'
  },
  {
    name: 'Carlos Ruiz',
    role: 'CTO de HealthSync',
    comment: 'Un socio tecnológico de verdad. Entregaron el proyecto a tiempo y con una calidad excepcional. El soporte post-lanzamiento ha sido impecable.',
    rating: 5,
    image: 'https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?auto=format&fit=crop&q=80&w=150'
  },
  {
    name: 'Marta López',
    role: 'Founder de EcoStream',
    comment: 'La mejor decisión que tomamos para nuestra infraestructura cloud. Muy recomendados por su profesionalidad y atención al detalle.',
    rating: 4,
    image: 'https://images.unsplash.com/photo-1438761681033-6461ffad8d80?auto=format&fit=crop&q=80&w=150'
  }
]
</script>

<template>
  <section id="testimonios" class="py-24 relative overflow-hidden">
    <!-- Decorative background elements -->
    <div class="absolute top-0 right-0 w-96 h-96 bg-indigo-500/5 rounded-full blur-3xl -z-10"></div>
    <div class="absolute bottom-0 left-0 w-96 h-96 bg-blue-500/5 rounded-full blur-3xl -z-10"></div>

    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="text-center mb-16">
        <h2 class="text-indigo-500 font-bold uppercase tracking-widest text-sm mb-3">Testimonios</h2>
        <p class="text-4xl font-black mb-4 dark:text-white text-slate-900">Lo que dicen de nosotros</p>
        <div class="w-20 h-1.5 bg-indigo-600 mx-auto rounded-full"></div>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
        <div 
          v-for="(testimonial, index) in testimonials" 
          :key="index"
          class="p-8 rounded-3xl dark:bg-slate-900/50 bg-white border dark:border-slate-800 border-slate-200 hover:shadow-2xl transition-all duration-300 group"
        >
          <!-- Stars -->
          <div class="flex gap-1 mb-6">
            <template v-for="star in 5" :key="star">
              <svg 
                class="w-5 h-5" 
                :class="star <= testimonial.rating ? 'text-yellow-400' : 'text-slate-300 dark:text-slate-700'"
                fill="currentColor" 
                viewBox="0 0 20 20"
              >
                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
              </svg>
            </template>
          </div>

          <p class="text-lg italic dark:text-slate-300 text-slate-600 mb-8 leading-relaxed">
            "{{ testimonial.comment }}"
          </p>

          <div class="flex items-center gap-4 mt-auto">
            <img 
              :src="testimonial.image" 
              :alt="testimonial.name"
              class="w-12 h-12 rounded-full object-cover ring-2 ring-indigo-500/20"
            />
            <div>
              <h4 class="font-bold dark:text-white text-slate-900">{{ testimonial.name }}</h4>
              <p class="text-sm dark:text-slate-500 text-slate-500">{{ testimonial.role }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
