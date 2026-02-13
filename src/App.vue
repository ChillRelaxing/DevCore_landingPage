<script setup lang="ts">
import { ref, onMounted, watch } from 'vue'
import Testimonials from './components/Testimonials.vue'
import Stats from './components/Stats.vue'

const isDark = ref(
  typeof window !== 'undefined' && (
    localStorage.getItem('theme') === 'dark' || 
    (!localStorage.getItem('theme') && window.matchMedia('(prefers-color-scheme: dark)').matches)
  )
)
const mobileMenuOpen = ref(false)

watch(isDark, (val) => { 
  if (val) {
    document.documentElement.classList.add('dark')
    localStorage.setItem('theme', 'dark')
  } else {
    document.documentElement.classList.remove('dark')
    localStorage.setItem('theme', 'light')
  }
}, { immediate: true })

onMounted(() => {
  // Theme is already initialized by the watch with immediate: true
})

const toggleDarkMode = () => {
  isDark.value = !isDark.value
}

const scrollToSection = (id: string) => {
  const el = document.getElementById(id)
  if (el) {
    el.scrollIntoView({ behavior: 'smooth' })
  }
  mobileMenuOpen.value = false
}

const navLinks = [
  { name: 'Servicios', id: 'servicios' },
  { name: 'Industria', id: 'industria' },
  { name: 'Sobre nosotros', id: 'nosotros' },
  { name: 'Estadísticas', id: 'estadisticas' },
  { name: 'Proyectos', id: 'proyectos' },
  { name: 'Testimonios', id: 'testimonios' },
  { name: 'Trabaja para nosotros', id: 'carreras' },
  { name: 'Perspectivas', id: 'perspectivas' },
]

const services = [
  { title: 'Desarrollo Web Custom', description: 'Creamos plataformas robustas y escalables utilizando las últimas tecnologías.', icon: 'M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4' },
  { title: 'Apps Móviles', description: 'Experiencias nativas e híbridas de alto rendimiento para iOS y Android.', icon: 'M12 18h.01M8 21h8a2 2 0 002-2V5a2 2 0 00-2-2H8a2 2 0 00-2 2v14a2 2 0 002 2z' },
  { title: 'Infraestructura Cloud', description: 'Implementación de servidores, despliegue continuo y arquitectura escalable.', icon: 'M5 12h14M5 12a2 2 0 01-2-2V6a2 2 0 012-2h14a2 2 0 012 2v4a2 2 0 01-2 2M5 12a2 2 0 00-2 2v4a2 2 0 002 2h14a2 2 0 002-2v-4a2 2 0 00-2-2m-2-4h.01M17 16h.01' },
]

const industries = ['DTE-System', 'E-commerce', 'Logistics', 'Big data']

const projects = [
  { name: 'Nexus Bank', category: 'Fintech', img: 'https://images.unsplash.com/photo-1551288049-bebda4e38f71?auto=format&fit=crop&q=80&w=800' },
  { name: 'HealthSync', category: 'Healthcare', img: 'https://images.unsplash.com/photo-1576091160550-2173dba999ef?auto=format&fit=crop&q=80&w=800' },
  { name: 'EcoStream', category: 'SaaS', img: 'https://images.unsplash.com/photo-1460925895917-afdab827c52f?auto=format&fit=crop&q=80&w=800' },
]

const contactForm = ref({
  name: '',
  email: '',
  message: ''
})

const isSubmitting = ref(false)
const showSuccess = ref(false)

const submitContactForm = async () => {
  isSubmitting.value = true
  // Simulate API call
  await new Promise(resolve => setTimeout(resolve, 1500))
  console.log('Form submitted:', contactForm.value)
  isSubmitting.value = false
  showSuccess.value = true
  
  // Reset form
  contactForm.value = {
    name: '',
    email: '',
    message: ''
  }
  
  // Hide success message after 5 seconds
  setTimeout(() => {
    showSuccess.value = false
  }, 5000)
}
</script>

<template>
  <div class="min-h-screen transition-colors duration-300 dark:bg-slate-950 dark:text-slate-100 bg-slate-50 text-slate-900 font-sans">
    
    <!-- Navbar -->
    <nav class="fixed w-full z-50 backdrop-blur-lg border-b dark:border-slate-800 border-slate-200 dark:bg-slate-950/80 bg-white/80">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex justify-between h-18 items-center">
          <div class="flex items-center gap-2 cursor-pointer group" @click="scrollToSection('hero')">
            <img src="./assets/logo/logo.png" width="150px" alt="DevCore Logo" class="h-10 w-auto transition-transform group-hover:scale-105 dark:invert dark:hue-rotate-180" />
          </div>

          <!-- Desktop Links -->
          <div class="hidden lg:flex space-x-6 items-center">
            <button v-for="link in navLinks" :key="link.id" @click="scrollToSection(link.id)" class="text-sm font-medium dark:text-slate-400 text-slate-600 hover:text-sky-600 dark:hover:text-sky-400 transition-colors">
              {{ link.name }}
            </button>
            <div class="h-6 w-px dark:bg-slate-800 bg-slate-200"></div>
            <button @click="toggleDarkMode" class="p-2 rounded-full hover:bg-slate-100 dark:hover:bg-slate-800 transition-colors">
              <svg v-if="isDark" xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-yellow-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364-6.364l-.707.707M6.343 17.657l-.707.707m12.728 0l-.707-.707M6.343 6.343l-.707-.707M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
              </svg>
              <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-slate-700" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
              </svg>
            </button>
            <button @click="scrollToSection('contacto')" class="bg-sky-600 hover:bg-sky-700 text-white px-6 py-2.5 rounded-full font-semibold transition-all shadow-lg shadow-sky-500/25 text-sm">
              Contactar
            </button>
          </div>

          <!-- Mobile Toggle -->
          <div class="lg:hidden flex items-center gap-4">
            <button @click="toggleDarkMode" class="p-2 rounded-full hover:bg-slate-100 dark:hover:bg-slate-800 transition-colors">
              <svg v-if="isDark" xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-yellow-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364-6.364l-.707.707M6.343 17.657l-.707.707m12.728 0l-.707-.707M6.343 6.343l-.707-.707M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
              </svg>
              <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-slate-700" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
              </svg>
            </button>
            <button @click="mobileMenuOpen = !mobileMenuOpen" class="dark:text-white text-slate-900 focus:outline-none">
              <svg class="h-7 w-7" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path v-if="!mobileMenuOpen" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
                <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
              </svg>
            </button>
          </div>
        </div>
      </div>

      <!-- Mobile Menu -->
      <transition enter-active-class="transition duration-200 ease-out" enter-from-class="opacity-0 -translate-y-4" enter-to-class="opacity-100 translate-y-0" leave-active-class="transition duration-150 ease-in" leave-from-class="opacity-100 translate-y-0" leave-to-class="opacity-0 -translate-y-4">
        <div v-if="mobileMenuOpen" class="lg:hidden dark:bg-slate-950 bg-white border-b dark:border-slate-800 border-slate-200">
          <div class="px-4 pt-4 pb-6 space-y-2">
            <button v-for="link in navLinks" :key="link.id" @click="scrollToSection(link.id)" class="block w-full text-left px-4 py-3 rounded-xl text-lg font-medium hover:bg-slate-50 dark:hover:bg-sky-900 transition-colors">
              {{ link.name }}
            </button>
            <div class="pt-4 px-4">
              <button @click="scrollToSection('contacto')" class="w-full bg-sky-600 text-white px-4 py-4 rounded-xl font-bold">
                Contactar
              </button>
            </div>
          </div>
        </div>
      </transition>
    </nav>

    <!-- Hero Section -->
    <header id="hero" class="relative pt-32 pb-20 lg:pt-52 lg:pb-40 overflow-hidden">
      <div class="absolute top-0 left-1/2 -translate-x-1/2 w-full max-w-7xl h-full -z-10 opacity-30">
        <div class="absolute top-0 right-0 w-96 h-96 bg-sky-500 rounded-full blur-[120px]"></div>
        <div class="absolute bottom-20 left-0 w-80 h-80 bg-blue-500 rounded-full blur-[100px]"></div>
      </div>

      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center lg:text-left flex flex-col lg:flex-row items-center gap-16">
        <div class="flex-1">
          <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-sky-500/10 text-sky-500 text-xs font-bold mb-8 border border-sky-500/20">
            <span class="relative flex h-2 w-2">
              <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-sky-400 opacity-75"></span>
              <span class="relative inline-flex rounded-full h-2 w-2 bg-sky-500"></span>
            </span>
            CONSTRUYENDO EL FUTURO DIGITAL
          </div>
          <h1 class="text-5xl lg:text-7xl font-black tracking-tight mb-6 leading-[1.1]">
            Ingeniería de <br />
            <span class="text-transparent bg-clip-text bg-gradient-to-r from-sky-500 to-blue-400">
              Software de Élite
            </span>
          </h1>
          <p class="text-xl dark:text-slate-400 text-slate-600 mb-10 max-w-2xl mx-auto lg:mx-0 leading-relaxed">
            En DevCore, transformamos ideas complejas en soluciones digitales excepcionales. Desde startups disruptivas hasta empresas globales, potenciamos tu crecimiento con tecnología de vanguardia.
          </p>
          <div class="flex flex-col sm:flex-row gap-4 justify-center lg:justify-start">
            <button @click="scrollToSection('proyectos')" class="px-8 py-4 rounded-2xl bg-sky-600 text-white font-bold hover:bg-sky-700 transition shadow-2xl shadow-sky-500/40 hover:-translate-y-1">
              Ver Proyectos
            </button>
          </div>
        </div>
        <div class="flex-1 relative">
          <div class="relative z-10 rounded-3xl overflow-hidden shadow-2xl border dark:border-slate-800 border-white/50 bg-slate-100/10 backdrop-blur-sm">
            <img src="https://images.unsplash.com/photo-1498050108023-c5249f4df085?auto=format&fit=crop&q=80&w=1200" alt="Dashboard Preview" class="w-full opacity-90" />
          </div>
          <div class="absolute -top-10 -right-10 w-40 h-40 bg-sky-600/20 rounded-full blur-3xl -z-10"></div>
          <div class="absolute -bottom-10 -left-10 w-40 h-40 bg-blue-600/20 rounded-full blur-3xl -z-10"></div>
        </div>
      </div>
    </header>

    <!-- Services Section -->
    <section id="servicios" class="py-24 relative">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center mb-20">
          <h2 class="text-sky-500 font-bold uppercase tracking-widest text-sm mb-3">Servicios</h2>
          <p class="text-4xl font-black mb-4">Soluciones End-to-End</p>
          <div class="w-20 h-1.5 bg-sky-600 mx-auto rounded-full"></div>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
          <div v-for="service in services" :key="service.title" class="p-10 rounded-3xl dark:bg-slate-900/50 bg-white border dark:border-slate-800 border-slate-200 hover:border-sky-500/50 transition-all group">
            <div class="w-14 h-14 bg-sky-600/10 rounded-2xl flex items-center justify-center mb-8 group-hover:scale-110 transition-transform">
              <svg class="w-8 h-8 text-sky-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" :d="service.icon" />
              </svg>
            </div>
            <h3 class="text-2xl font-bold mb-4">{{ service.title }}</h3>
            <p class="dark:text-slate-400 text-slate-600 leading-relaxed mb-6">
              {{ service.description }}
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- Industry Section -->
    <section id="industria" class="py-24 dark:bg-slate-900 bg-sky-600 text-white overflow-hidden">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex flex-col lg:flex-row items-center gap-16">
          <div class="flex-1">
            <h2 class="text-sky-300 font-bold uppercase tracking-widest text-sm mb-3">Industrias</h2>
            <p class="text-4xl font-black mb-6 leading-tight">Expertos en mercados verticales de alta demanda</p>
            <p class="text-sky-100 mb-8 text-lg opacity-80">
              Entendemos los retos específicos de cada sector. Nuestra experiencia nos permite acelerar el desarrollo con arquitecturas probadas y adaptadas a las regulaciones de cada industria.
            </p>
            <div class="grid grid-cols-2 gap-4">
              <div v-for="industry in industries" :key="industry" class="flex items-center gap-3 bg-white/10 px-5 py-3 rounded-xl backdrop-blur-sm border border-white/10 hover:bg-white/20 transition-colors">
                <svg class="w-5 h-5 text-sky-300" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
                </svg>
                <span class="font-medium">{{ industry }}</span>
              </div>
            </div>
          </div>
          <div class="flex-1 flex justify-center">
            <div class="grid grid-cols-2 gap-6 rotate-12 scale-110 opacity-20 lg:opacity-100">
               <div class="w-40 h-40 bg-white rounded-3xl animate-pulse"></div>
               <div class="w-40 h-40 bg-sky-300 rounded-3xl translate-y-10"></div>
               <div class="w-40 h-40 bg-sky-400 rounded-3xl -translate-y-10"></div>
               <div class="w-40 h-40 bg-white/50 rounded-3xl"></div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- About Us Section -->
    <section id="nosotros" class="py-24">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex flex-col lg:flex-row gap-20 items-center">
          <div class="flex-1 grid grid-cols-2 gap-4">
            <img src="https://images.unsplash.com/photo-1522071820081-009f0129c71c?auto=format&fit=crop&q=80&w=600" class="rounded-3xl h-64 w-full object-cover" />
            <div class="bg-sky-600 rounded-3xl h-64 flex flex-col items-center justify-center p-6 text-white text-center">
              <span class="text-5xl font-black"><img class="invert" src="./assets/img/calidad.png" width="100px" alt=""></span>
            </div>
            <div class="bg-slate-200 dark:bg-slate-800 rounded-3xl h-64 flex flex-col items-center justify-center p-6 text-center">
              <span class="text-5xl font-black"><img class="[filter:invert(48%)_sepia(70%)_saturate(2476%)_hue-rotate(167deg)_brightness(94%)_contrast(101%)]" src="./assets/img/codigo.png" width="100px" alt=""></span>
            </div>
            <img src="https://images.unsplash.com/photo-1552664730-d307ca884978?auto=format&fit=crop&q=80&w=600" class="rounded-3xl h-64 w-full object-cover" />
          </div>
          <div class="flex-1">
            <h2 class="text-sky-500 font-bold uppercase tracking-widest text-sm mb-3">Sobre Nosotros</h2>
            <h3 class="text-4xl font-black mb-6">Obsesionados con la Calidad y el Código Limpio</h3>
            <p class="text-lg dark:text-slate-400 text-slate-600 mb-8 leading-relaxed">
              DevCore nació con una misión clara: elevar el estándar del desarrollo de software en la región. No somos solo una agencia, somos un socio tecnológico comprometido con el éxito a largo plazo de nuestros clientes.
            </p>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-10">
              <div class="p-6 rounded-2xl bg-sky-500/5 border border-sky-500/10">
                <h4 class="text-sky-600 dark:text-sky-400 font-bold mb-2 flex items-center gap-2">
                  <svg class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
                  </svg>
                  Misión
                </h4>
                <p class="text-sm dark:text-slate-400 text-slate-600 leading-relaxed">
                  Impulsar la transformación digital mediante soluciones tecnológicas innovadoras, escalables y de alta calidad que generen un impacto real.
                </p>
              </div>
              <div class="p-6 rounded-2xl bg-blue-500/5 border border-blue-500/10">
                <h4 class="text-blue-600 dark:text-blue-400 font-bold mb-2 flex items-center gap-2">
                  <svg class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
                  </svg>
                  Visión
                </h4>
                <p class="text-sm dark:text-slate-400 text-slate-600 leading-relaxed">
                  Ser el socio tecnológico líder global, reconocido por la excelencia en ingeniería y la capacidad de resolver los desafíos más complejos.
                </p>
              </div>
            </div>

            <ul class="space-y-4">
              <li class="flex items-start gap-4">
                <div class="w-6 h-6 rounded-full bg-sky-500 flex-shrink-0 flex items-center justify-center mt-1">
                   <svg class="w-4 h-4 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path d="M5 13l4 4L19 7" stroke-width="3"/></svg>
                </div>
                <div>
                  <h4 class="font-bold">Mentalidad Product-First</h4>
                  <p class="dark:text-slate-500 text-slate-500 text-sm">No solo escribimos código, entendemos tu modelo de negocio.</p>
                </div>
              </li>
              <li class="flex items-start gap-4">
                <div class="w-6 h-6 rounded-full bg-sky-500 flex-shrink-0 flex items-center justify-center mt-1">
                   <svg class="w-4 h-4 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path d="M5 13l4 4L19 7" stroke-width="3"/></svg>
                </div>
                <div>
                  <h4 class="font-bold">Metodologías Ágiles Reales</h4>
                  <p class="dark:text-slate-500 text-slate-500 text-sm">Entregas incrementales cada dos semanas para máxima visibilidad.</p>
                </div>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </section>

    <Stats />

    <!-- Projects Section -->
    <section id="proyectos" class="py-24 dark:bg-slate-900/30 bg-slate-100">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex flex-col md:flex-row justify-between items-end mb-16">
          <div>
            <h2 class="text-sky-500 font-bold uppercase tracking-widest text-sm mb-3">Portafolio</h2>
            <p class="text-4xl font-black">Proyectos Destacados</p>
          </div>
          <button class="hidden md:block text-sky-500 font-bold hover:underline">Ver todos los casos de éxito →</button>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
          <div v-for="project in projects" :key="project.name" class="group cursor-pointer">
            <div class="relative overflow-hidden rounded-3xl aspect-[4/5] mb-6 shadow-xl">
              <img :src="project.img" :alt="project.name" class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-700" />
              <div class="absolute inset-0 bg-gradient-to-t from-slate-900 via-transparent to-transparent opacity-80"></div>
              <div class="absolute bottom-8 left-8">
                <span class="px-3 py-1 rounded-full bg-white/20 backdrop-blur-md text-white text-xs font-bold mb-3 inline-block border border-white/20">
                  {{ project.category }}
                </span>
                <h4 class="text-2xl font-bold text-white">{{ project.name }}</h4>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Testimonials Section -->
    <Testimonials />

    <!-- Careers Section -->
    <section id="carreras" class="py-24">
      <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
        <div class="bg-gradient-to-br from-sky-600 to-blue-700 rounded-[3rem] p-12 lg:p-20 text-white shadow-2xl relative overflow-hidden">
          <div class="absolute -top-20 -right-20 w-64 h-64 bg-white/10 rounded-full blur-3xl"></div>
          <div class="relative z-10">
            <h2 class="text-4xl lg:text-5xl font-black mb-8 leading-tight">¿Eres un apasionado del código?</h2>
            <p class="text-xl text-sky-100 mb-10 max-w-2xl mx-auto opacity-90">
              Estamos buscando talento excepcional para unirse a nuestra revolución tecnológica. Trabaja de forma remota, con los mejores beneficios y un equipo que te desafiará cada día.
            </p>
            <button class="bg-white text-sky-600 px-10 py-4 rounded-2xl font-black hover:bg-slate-100 transition shadow-xl">
              Ver Vacantes Abiertas
            </button>
          </div>
        </div>
      </div>
    </section>

    <!-- Perspectives Section -->
    <section id="perspectivas" class="py-24">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center mb-16">
          <h2 class="text-sky-500 font-bold uppercase tracking-widest text-sm mb-3">Perspectivas</h2>
          <p class="text-4xl font-black">Blog & Insights</p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-10">
          <div class="group">
            <div class="rounded-2xl overflow-hidden mb-6 aspect-video">
              <img src="https://images.unsplash.com/photo-1550751827-4bd374c3f58b?auto=format&fit=crop&q=80&w=800" class="w-full h-full object-cover group-hover:rotate-2 group-hover:scale-105 transition-all duration-500" />
            </div>
            <span class="text-sky-500 text-sm font-bold uppercase">Tecnología</span>
            <h4 class="text-xl font-bold mt-2 mb-4 group-hover:text-sky-500 transition-colors">El impacto de WebAssembly en el desarrollo frontend moderno</h4>
            <p class="dark:text-slate-400 text-slate-600 text-sm leading-relaxed">
              Exploramos cómo WASM está permitiendo que aplicaciones de alto rendimiento se ejecuten en el navegador...
            </p>
          </div>
          <div class="group">
            <div class="rounded-2xl overflow-hidden mb-6 aspect-video">
              <img src="https://images.unsplash.com/photo-1517245386807-bb43f82c33c4?auto=format&fit=crop&q=80&w=800" class="w-full h-full object-cover group-hover:rotate-2 group-hover:scale-105 transition-all duration-500" />
            </div>
            <span class="text-sky-500 text-sm font-bold uppercase">Cultura</span>
            <h4 class="text-xl font-bold mt-2 mb-4 group-hover:text-sky-500 transition-colors">Cómo mantenemos la cohesión en equipos 100% remotos</h4>
            <p class="dark:text-slate-400 text-slate-600 text-sm leading-relaxed">
              Nuestras mejores prácticas para fomentar la colaboración y el sentido de pertenencia a distancia...
            </p>
          </div>
          <div class="group">
            <div class="rounded-2xl overflow-hidden mb-6 aspect-video">
              <img src="https://images.unsplash.com/photo-1555066931-4365d14bab8c?auto=format&fit=crop&q=80&w=800" class="w-full h-full object-cover group-hover:rotate-2 group-hover:scale-105 transition-all duration-500" />
            </div>
            <span class="text-sky-500 text-sm font-bold uppercase">Tutorial</span>
            <h4 class="text-xl font-bold mt-2 mb-4 group-hover:text-sky-500 transition-colors">Escalando APIs con NestJS y Microservicios</h4>
            <p class="dark:text-slate-400 text-slate-600 text-sm leading-relaxed">
              Una guía técnica sobre patrones de diseño para arquitecturas escalables y resilientes...
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contacto" class="py-24 relative overflow-hidden">
      <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-full max-w-4xl h-full -z-10 opacity-20">
        <div class="absolute top-0 right-0 w-80 h-80 bg-sky-500 rounded-full blur-[100px] animate-pulse"></div>
        <div class="absolute bottom-0 left-0 w-80 h-80 bg-blue-500 rounded-full blur-[100px] animate-pulse"></div>
      </div>

      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="max-w-4xl mx-auto bg-white dark:bg-slate-900 rounded-[2.5rem] shadow-2xl border border-slate-200 dark:border-slate-800 overflow-hidden flex flex-col md:flex-row">
          <div class="flex-1 bg-sky-600 p-12 text-white">
            <h2 class="text-3xl font-black mb-6">Hablemos de tu próximo gran proyecto</h2>
            <p class="text-sky-100 mb-10 leading-relaxed">
              Estamos listos para escucharte y convertir tus ideas en realidad. Déjanos un mensaje y nuestro equipo de expertos se pondrá en contacto contigo en menos de 24 horas.
            </p>
            
            <div class="space-y-6">
              <div class="flex items-center gap-4">
                <div class="w-12 h-12 bg-white/10 rounded-xl flex items-center justify-center">
                  <svg class="w-6 h-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
                  </svg>
                </div>
                <div>
                  <p class="text-sm text-sky-200 font-bold uppercase">Email</p>
                  <p class="font-bold">devcore@gmail.com</p>
                </div>
              </div>
              <div class="flex items-center gap-4">
                <div class="w-12 h-12 bg-white/10 rounded-xl flex items-center justify-center">
                  <svg class="w-6 h-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
                  </svg>
                </div>
                <div>
                  <p class="text-sm text-sky-200 font-bold uppercase">Oficina</p>
                  <p class="font-bold">2ª Calle Oriente y 2ª Avenida Norte, San Miguel Centro.</p>
                </div>
              </div>
            </div>
          </div>
          
          <div class="flex-[1.5] p-12">
            <form v-if="!showSuccess" @submit.prevent="submitContactForm" class="space-y-6">
              <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
                <div>
                  <label class="block text-sm font-bold mb-2 ml-1">Nombre</label>
                  <input v-model="contactForm.name" required type="text" placeholder="Tu nombre" class="w-full bg-slate-50 dark:bg-slate-800 border-none rounded-2xl px-5 py-4 focus:ring-2 focus:ring-sky-500 transition-all" />
                </div>
                <div>
                  <label class="block text-sm font-bold mb-2 ml-1">Email</label>
                  <input v-model="contactForm.email" required type="email" placeholder="tu@email.com" class="w-full bg-slate-50 dark:bg-slate-800 border-none rounded-2xl px-5 py-4 focus:ring-2 focus:ring-sky-500 transition-all" />
                </div>
              </div>
              <div>
                <label class="block text-sm font-bold mb-2 ml-1">Mensaje</label>
                <textarea v-model="contactForm.message" required rows="4" placeholder="¿En qué podemos ayudarte?" class="w-full bg-slate-50 dark:bg-slate-800 border-none rounded-2xl px-5 py-4 focus:ring-2 focus:ring-sky-500 transition-all resize-none"></textarea>
              </div>
              <button :disabled="isSubmitting" type="submit" class="w-full bg-sky-600 text-white py-5 rounded-2xl font-black text-lg hover:bg-sky-700 transition shadow-xl shadow-sky-500/30 flex items-center justify-center gap-3 disabled:opacity-70">
                <svg v-if="isSubmitting" class="animate-spin h-5 w-5 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                  <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                  <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                </svg>
                {{ isSubmitting ? 'Enviando...' : 'Enviar Mensaje' }}
              </button>
            </form>
            
            <div v-else class="h-full flex flex-col items-center justify-center text-center py-12">
              <div class="w-20 h-20 bg-green-500/10 rounded-full flex items-center justify-center text-green-500 mb-6">
                <svg class="w-10 h-10" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M5 13l4 4L19 7" />
                </svg>
              </div>
              <h3 class="text-2xl font-black mb-2">¡Mensaje Recibido!</h3>
              <p class="text-slate-500 dark:text-slate-400">Gracias por contactarnos. Te responderemos lo antes posible.</p>
              <button @click="showSuccess = false" class="mt-8 text-sky-600 font-bold hover:underline">Enviar otro mensaje</button>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="dark:bg-slate-950 bg-slate-900 text-white pt-20 pb-10 border-t dark:border-slate-800">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-12 mb-16">
          <div class="col-span-1 lg:col-span-1">
            <div class="flex items-center gap-2 mb-6">
              <img src="./assets/logo/logo.png" alt="DevCore Logo" class="h-10 w-auto invert hue-rotate-180" />
            </div>
            <p class="text-slate-400 text-sm leading-relaxed mb-6">
              Engineering the digital future. Expert software development for visionary companies.
            </p>
            <div class="flex gap-4">
               <a href="#" class="w-10 h-10 rounded-full bg-slate-800 flex items-center justify-center hover:bg-sky-600 transition-colors">
                  <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M24 4.557c-.883.392-1.832.656-2.828.775 1.017-.609 1.798-1.574 2.165-2.724-.951.564-2.005.974-3.127 1.195-.897-.957-2.178-1.555-3.594-1.555-3.179 0-5.515 2.966-4.797 6.045-4.091-.205-7.719-2.165-10.148-5.144-1.29 2.213-.669 5.108 1.523 6.574-.806-.026-1.566-.247-2.229-.616-.054 2.281 1.581 4.415 3.949 4.89-.693.188-1.452.232-2.224.084.626 1.956 2.444 3.379 4.6 3.419-2.07 1.623-4.678 2.348-7.29 2.04 2.179 1.397 4.768 2.212 7.548 2.212 9.142 0 14.307-7.721 13.995-14.646.962-.695 1.797-1.562 2.457-2.549z"/></svg>
               </a>
               <a href="#" class="w-10 h-10 rounded-full bg-slate-800 flex items-center justify-center hover:bg-sky-600 transition-colors">
                  <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.761 0 5-2.239 5-5v-14c0-2.761-2.239-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z"/></svg>
               </a>
            </div>
          </div>
          <div>
            <h4 class="font-bold mb-6">Compañía</h4>
            <ul class="space-y-4 text-slate-400 text-sm">
              <li><a href="#" @click.prevent="scrollToSection('nosotros')" class="hover:text-white transition">Sobre Nosotros</a></li>
              <li><a href="#" @click.prevent="scrollToSection('carreras')" class="hover:text-white transition">Carreras</a></li>
              <li><a href="#" @click.prevent="scrollToSection('proyectos')" class="hover:text-white transition">Casos de Éxito</a></li>
              <li><a href="#" class="hover:text-white transition">Prensa</a></li>
            </ul>
          </div>
          <div>
            <h4 class="font-bold mb-6">Servicios</h4>
            <ul class="space-y-4 text-slate-400 text-sm">
              <li><a href="#" class="hover:text-white transition">Desarrollo Web</a></li>
              <li><a href="#" class="hover:text-white transition">Cloud & DevOps</a></li>
              <li><a href="#" class="hover:text-white transition">Diseño UI/UX</a></li>
              <li><a href="#" class="hover:text-white transition">Desarrollo Movil</a></li>
            </ul>
          </div>
        </div>
        <div class="border-t border-slate-800 pt-8 flex flex-col md:flex-row justify-between items-center gap-4">
          <p class="text-slate-500 text-xs">© 2026 DevCore Inc. Todos los derechos reservados.</p>
          <div class="flex gap-6 text-slate-500 text-xs">
            <span href="#" class="hover:text-white transition">Términos</span>
            <span href="#" class="hover:text-white transition">Privacidad</span>
            <span href="#" class="hover:text-white transition">Cookies</span>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<style>
@keyframes blob {
  0% { transform: translate(0px, 0px) scale(1); }
  33% { transform: translate(30px, -50px) scale(1.1); }
  66% { transform: translate(-20px, 20px) scale(0.9); }
  100% { transform: translate(0px, 0px) scale(1); }
}
.animate-blob {
  animation: blob 7s infinite;
}
</style>