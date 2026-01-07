<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue';

const isMenuOpen = ref(false);
const scrolled = ref(false);
const activeCategory = ref('All');

const navLinks = [
  { name: 'Home', href: '#hero' },
  { name: 'Stack', href: '#stack' },
  { name: 'Projects', href: '#projects' },
  { name: 'Contact', href: '#contact' },
];

const categories = ['All', 'Backend', 'Database', 'Frontend', 'Tools'];

const techStack = [
  { name: 'Java', category: 'Backend', icon: 'devicon-java-plain', color: '#ED8B00' },
  { name: 'Spring Boot', category: 'Backend', icon: 'devicon-spring-original', color: '#6DB33F' },
  { name: 'Hibernate/JPA', category: 'Backend', icon: 'devicon-hibernate-plain', color: '#59666C' },
  { name: 'Vue.js', category: 'Frontend', icon: 'devicon-vuejs-plain', color: '#42b883' },
  { name: 'Elasticsearch', category: 'Backend', icon: 'devicon-elasticsearch-plain', color: '#00BFB3' },
  { name: 'MongoDB', category: 'Database', icon: 'devicon-mongodb-plain', color: '#4EA94B' },
  { name: 'Kafka', category: 'Backend', icon: 'devicon-apachekafka-original', color: '#ffffff' },
  { name: 'MySQL', category: 'Database', icon: 'devicon-mysql-plain', color: '#4479A1' },
  { name: 'Redis', category: 'Database', icon: 'devicon-redis-plain', color: '#DC382D' },
  { name: 'PostgreSQL', category: 'Database', icon: 'devicon-postgresql-plain', color: '#336791' },
  { name: 'Docker', category: 'Tools', icon: 'devicon-docker-plain', color: '#2496ED' },
  { name: 'Git', category: 'Tools', icon: 'devicon-git-plain', color: '#F05032' },
  { name: 'Maven', category: 'Tools', icon: 'devicon-maven-plain', color: '#C71A36' },
  { name: 'Gradle', category: 'Tools', icon: 'devicon-gradle-original', color: '#0889a6' },
  { name: 'JavaScript', category: 'Frontend', icon: 'devicon-javascript-plain', color: '#F7DF1E' },
  { name: 'TypeScript', category: 'Frontend', icon: 'devicon-typescript-plain', color: '#2496ED' },
  { name: 'HTML5', category: 'Frontend', icon: 'devicon-html5-plain', color: '#E34F26' },
  { name: 'Tailwind CSS', category: 'Frontend', icon: 'devicon-tailwindcss-original', color: '#06B6D4' },
  { name: 'Figma', category: 'Frontend', icon: 'devicon-figma-plain', color: '#F24E1E' },
  { name: 'Linux', category: 'Tools', icon: 'devicon-linux-plain', color: '#ffffff' },
];

const projects = [
  {
    title: 'LogiFlow - Inventory Management Platform',
    period: '12.2025 - Present',
    link: 'https://github.com/kzhunmax/logiflow',
    shortDesc: 'Modular monolith application for warehouse management with product catalogs, inventory tracking, and order processing.',
    bullets: [
      'Separated code into modules: catalog, inventory, orders, shared.',
      'Built frontend with Vue.js 3.',
      'Developed backend with Java 25 and Spring Boot.',
      'Used MongoDB for product attributes and PostgreSQL for transactional data (inventory, orders, authentication).',
    ],
    icon: 'pi pi-box',
    color: 'text-sky-400',
    borderColor: 'border-sky-400'
  },
  {
    title: 'JobHunter - Job Search & Application Platform',
    period: '09.2025 - 12.2025',
    link: 'https://github.com/kzhunmax/JobHunter',
    shortDesc: 'Backend application for job listings, applications, and user management.',
    bullets: [
      'Implemented OAuth2 authentication with Google and GitHub providers using Spring Security.',
      'Added JWT stateless authentication and role-based access control.',
      'Integrated Elasticsearch for job search and filtering.',
      'Added Stripe API for subscription payments.',
      'Used AWS S3 (via Supabase) for resume storage with upload validation.',
      'Implemented asynchronous email notifications with Apache Kafka.',
      'Applied rate limiting with Bucket4j and Redis.',
      'Containerized services with Docker Compose (PostgreSQL, Redis, Elasticsearch, Kafka).',
      'Wrote tests with JUnit 5, Mockito, and Testcontainers.',
    ],
    icon: 'pi pi-briefcase',
    color: 'text-indigo-400',
    borderColor: 'border-indigo-400'
  },
  {
    title: 'Apartment Finder Platform',
    period: '2024 - 2025',
    link: null,
    shortDesc: 'Telegram bot and backend for apartment search based on user descriptions. Collaborated with senior full-stack developer and junior DevOps.',
    bullets: [
      'Developed backend services with Spring Boot.',
      'Used Apache Kafka for event-driven architecture and data processing.',
      'Integrated Elasticsearch for full-text search and filtering of listings.',
      'Added third-party AI service for query-listing relevance scoring.',
      'Wrote integration tests with Testcontainers.',
      'Built Docker images with multi-stage builds.',
    ],
    icon: 'pi pi-home',
    color: 'text-green-400',
    borderColor: 'border-green-400'
  },
];

const filteredStack = computed(() => {
  if (activeCategory.value === 'All') return techStack;
  return techStack.filter(item => item.category === activeCategory.value);
});

const handleScroll = () => {
  scrolled.value = window.scrollY > 20;
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
});
</script>

<template>
  <div class="min-h-screen bg-slate-900 text-slate-100 font-sans selection:bg-sky-500 selection:text-white overflow-x-hidden">

    <div class="fixed inset-0 z-0 pointer-events-none">
      <div class="absolute top-0 left-0 w-full h-full bg-[radial-gradient(ellipse_at_top,var(--tw-gradient-stops))] from-slate-800 via-slate-900 to-black opacity-80"></div>
      <div class="absolute top-[-10%] right-[-5%] w-96 h-96 bg-sky-500/20 rounded-full blur-3xl animate-pulse-slow"></div>
      <div class="absolute bottom-[-10%] left-[-5%] w-96 h-96 bg-indigo-500/20 rounded-full blur-3xl animate-pulse-slow delay-1000"></div>
    </div>

    <nav
      class="fixed w-full z-50 transition-all duration-300 border-b border-transparent"
      :class="scrolled ? 'bg-slate-900/80 backdrop-blur-md border-white/10 py-3 shadow-lg' : 'bg-transparent py-6'"
    >
      <div class="max-w-7xl mx-auto px-6 flex justify-between items-center">
        <a href="#" class="text-2xl font-extrabold tracking-tighter hover:text-sky-400 transition-colors">
          MK<span class="text-sky-500">.</span>
        </a>

        <div class="hidden md:flex gap-8 text-sm font-medium text-slate-300">
          <a
            v-for="link in navLinks"
            :key="link.name"
            :href="link.href"
            class="hover:text-sky-400 transition-colors relative group"
          >
            {{ link.name }}
            <span class="absolute -bottom-1 left-0 w-0 h-0.5 bg-sky-400 transition-all duration-300 group-hover:w-full"></span>
          </a>
        </div>

        <button @click="isMenuOpen = !isMenuOpen" class="md:hidden text-2xl text-slate-200 hover:text-white focus:outline-none z-50">
          <i :class="isMenuOpen ? 'pi pi-times' : 'pi pi-bars'"></i>
        </button>
      </div>

      <transition
        enter-active-class="transition duration-200 ease-out"
        enter-from-class="opacity-0 -translate-y-2"
        enter-to-class="opacity-100 translate-y-0"
        leave-active-class="transition duration-150 ease-in"
        leave-from-class="opacity-100 translate-y-0"
        leave-to-class="opacity-0 -translate-y-2"
      >
        <div v-if="isMenuOpen" class="md:hidden absolute top-full left-0 w-full bg-slate-900/95 backdrop-blur-xl border-t border-slate-700 shadow-2xl">
          <div class="flex flex-col p-6 gap-4">
            <a
              v-for="link in navLinks"
              :key="link.name"
              :href="link.href"
              @click="isMenuOpen = false"
              class="text-lg font-medium text-slate-300 hover:text-sky-400 hover:pl-2 transition-all"
            >
              {{ link.name }}
            </a>
          </div>
        </div>
      </transition>
    </nav>

    <!-- Hero Section -->
    <section id="hero" class="relative min-h-screen flex items-center justify-center px-6 pt-20">
      <div class="max-w-6xl w-full grid md:grid-cols-2 gap-12 items-center z-10">

        <!-- Text Content -->
        <div class="space-y-8 animate-fade-in">
          <div class="inline-flex items-center gap-2 px-3 py-1.5 rounded-full bg-slate-800/80 border border-slate-700 text-xs font-semibold text-sky-400 backdrop-blur-sm">
            <span class="relative flex h-2 w-2">
              <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-sky-400 opacity-75"></span>
              <span class="relative inline-flex rounded-full h-2 w-2 bg-sky-500"></span>
            </span>
            Available for new opportunities
          </div>

          <h1 class="text-5xl md:text-7xl font-bold leading-tight tracking-tight">
            Hi, I'm
            <span class="text-transparent bg-clip-text bg-linear-to-r from-sky-400 via-blue-500 to-indigo-500">
              Maksym Korshun
            </span>
          </h1>

          <p class="text-lg md:text-xl text-slate-400 max-w-lg leading-relaxed">
            A <strong>Full-Stack Developer</strong> specializing in Java backend and full-stack development with Vue.js. Demonstrated ability to design and implement high-performance services using Spring Boot and relational/NoSQL databases. Experienced in creating modern web applications with Vue.js frontend, robust REST APIs, and integrated OAuth2 security. Passionate about clean code practices and thorough testing (JUnit, Mockito, Testcontainers)
          </p>
          <div class="flex flex-wrap gap-4 pt-2">
            <a href="#stack" class="px-7 py-3.5 bg-sky-500 hover:bg-sky-400 text-white font-bold rounded-lg transition-all shadow-lg shadow-sky-500/25 transform hover:-translate-y-1">
              View My Stack
            </a>
            <a href="#contact" class="px-7 py-3.5 bg-white/5 hover:bg-white/10 text-white font-semibold rounded-lg border border-white/10 transition-all backdrop-blur-sm flex items-center gap-2 group">
              Contact Me
              <i class="pi pi-arrow-right text-xs transition-transform group-hover:translate-x-1"></i>
            </a>
          </div>

          <!-- Social Icons -->
          <div class="flex gap-6 pt-4 text-2xl text-slate-400">
            <a href="https://github.com/kzhunmax" target="_blank" class="hover:text-white hover:scale-110 transition-all"><i class="pi pi-github"></i></a>
            <a href="https://linkedin.com/in/maksym-korshun" target="_blank" class="hover:text-sky-400 hover:scale-110 transition-all"><i class="pi pi-linkedin"></i></a>
            <a href="mailto:korshunmax82@gmail.com" class="hover:text-red-400 hover:scale-110 transition-all"><i class="pi pi-envelope"></i></a>
          </div>
        </div>

        <div class="hidden md:block perspective-1000">
          <img src="./assets/image.png" alt="My Photo" class="w-full rounded-3xl shadow-2xl border border-white/10 transform hover:rotate-y-6 hover:rotate-x-3 transition-transform duration-500" />
        </div>
      </div>
    </section>

    <!-- Tech Stack Section -->
    <section id="stack" class="py-24 px-6 relative z-10">
      <div class="max-w-6xl mx-auto">
        <div class="text-center mb-16">
          <h2 class="text-3xl md:text-5xl font-bold mb-6 bg-clip-text text-transparent bg-linear-to-b from-white to-slate-400">My Tech Stack</h2>
          <div class="h-1.5 w-24 bg-sky-500 mx-auto rounded-full"></div>
        </div>

        <div class="flex flex-wrap justify-center gap-3 mb-12">
          <button
            v-for="cat in categories"
            :key="cat"
            @click="activeCategory = cat"
            class="px-6 py-2.5 rounded-full text-sm font-semibold transition-all duration-300 border backdrop-blur-md"
            :class="activeCategory === cat ? 'bg-sky-500/90 text-white border-sky-400 shadow-[0_0_15px_rgba(14,165,233,0.4)] transform scale-105' : 'bg-slate-800/50 text-slate-400 border-slate-700 hover:border-sky-500/50 hover:text-white'"
          >
            {{ cat }}
          </button>
        </div>

        <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 gap-6">
          <transition-group
            enter-active-class="transition duration-300 ease-out"
            enter-from-class="opacity-0 scale-90"
            enter-to-class="opacity-100 scale-100"
            leave-active-class="absolute opacity-0"
          >
            <div
              v-for="item in filteredStack"
              :key="item.name"
              class="group relative bg-slate-800/40 backdrop-blur-md p-6 rounded-2xl flex flex-col items-center gap-4 border border-white/5 hover:bg-slate-700/50 hover:border-sky-500/30 transition-all duration-300 hover:-translate-y-2 cursor-default"
            >
              <i
                :class="item.icon"
                class="text-6xl transition-transform duration-300 group-hover:scale-110 drop-shadow-lg"
                :style="{ color: item.color }"
              ></i>
              <span class="font-bold text-slate-300 group-hover:text-white transition-colors">{{ item.name }}</span>
              <div class="absolute inset-0 rounded-2xl bg-sky-500/5 opacity-0 group-hover:opacity-100 transition-opacity pointer-events-none"></div>
            </div>
          </transition-group>
        </div>
      </div>
    </section>

    <!-- Projects Section -->
    <section id="projects" class="py-24 px-6 relative z-10">
      <div class="max-w-4xl mx-auto">
        <div class="bg-slate-800/40 backdrop-blur-xl p-8 md:p-12 rounded-3xl border border-white/5 shadow-2xl relative overflow-hidden">
          <div class="absolute top-0 right-0 w-64 h-64 bg-indigo-500/10 rounded-full blur-3xl pointer-events-none"></div>

          <h2 class="text-3xl md:text-4xl font-bold mb-12 flex items-center gap-4">
            <span class="flex shrink-0 items-center justify-center w-14 h-14 bg-sky-500/10 rounded-xl text-sky-400 border border-sky-500/20">
              <i class="pi pi-folder-open text-2xl"></i>
            </span>
            Projects
          </h2>

          <div class="space-y-12">
            <div
              v-for="(project, index) in projects"
              :key="index"
              class="relative pl-8 md:pl-12 border-l-2 border-slate-700 hover:border-sky-500/50 transition-colors duration-300"
            >
              <div
                class="absolute -left-2.25 top-0 w-4 h-4 rounded-full bg-slate-900 border-2 transition-colors duration-300"
                :class="project.borderColor"
              ></div>

              <div class="flex flex-wrap justify-between items-baseline mb-2">
                <h3 class="text-xl md:text-2xl font-bold text-white">
                  <a v-if="project.link" :href="project.link" target="_blank" class="hover:text-sky-400 transition-colors">
                    {{ project.title }} <i class="pi pi-external-link text-sm"></i>
                  </a>
                  <span v-else>{{ project.title }}</span>
                </h3>
                <span class="text-sm font-mono text-slate-400 bg-slate-700/50 px-2 py-1 rounded">{{ project.period }}</span>
              </div>

              <p class="text-slate-300 leading-relaxed mb-4">{{ project.shortDesc }}</p>

              <ul class="list-disc pl-6 space-y-2 text-slate-400">
                <li v-for="bullet in project.bullets" :key="bullet">{{ bullet }}</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="py-24 px-6 relative z-10">
      <div class="max-w-3xl mx-auto text-center">
        <h2 class="text-4xl md:text-5xl font-bold mb-8">Let's Work Together</h2>
        <p class="text-slate-400 mb-12 text-lg md:text-xl max-w-2xl mx-auto">
          I'm currently looking for new opportunities in backend/full-stack development. Whether you have a question or just want to say hi, my inbox is always open.
        </p>

        <div class="flex flex-col md:flex-row justify-center gap-6">
          <a href="mailto:korshunmax82@gmail.com" class="px-8 py-5 bg-linear-to-r from-sky-600 to-blue-600 hover:from-sky-500 hover:to-blue-500 text-white rounded-xl text-lg font-bold shadow-lg shadow-sky-900/50 transform hover:-translate-y-1 transition-all flex items-center justify-center gap-3">
            <i class="pi pi-envelope text-xl"></i>
            Say Hello
          </a>
          <a href="https://linkedin.com/in/maksym-korshun" target="_blank" class="px-8 py-5 bg-slate-800 hover:bg-slate-700 text-white rounded-xl text-lg font-bold border border-slate-700 hover:border-slate-500 transition-all flex items-center justify-center gap-3">
            <i class="pi pi-linkedin text-xl text-sky-400"></i>
            LinkedIn
          </a>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="py-8 text-center border-t border-slate-800/50 bg-slate-900/50 backdrop-blur-sm">
      <p class="text-slate-500 text-sm">
        &copy; 2026 Maksym Korshun. All rights reserved.
      </p>
    </footer>

  </div>
</template>

<style>
@keyframes pulse-slow {
  0%, 100% { opacity: 0.4; }
  50% { opacity: 0.7; }
}
.animate-pulse-slow {
  animation: pulse-slow 8s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}

@keyframes fade-in {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}
.animate-fade-in {
  animation: fade-in 1s ease-out forwards;
}

.perspective-1000 {
  perspective: 1000px;
}
</style>
