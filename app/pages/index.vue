<script setup lang="ts">
import { computed, onMounted, ref, watch } from 'vue'

type Language = 'fr' | 'en'
type Theme = 'light' | 'dark'

const currentLanguage = ref<Language>('fr')
const currentTheme = ref<Theme>('light')
const menuOpen = ref(false)

const locale = {
  fr: {
    nav: {
      home: 'Accueil',
      about: 'À propos',
      skills: 'Compétences',
      projects: 'Projets',
      education: 'Formation',
      contact: 'Contact'
    },
    badge: 'BONJOUR, JE SUIS',
    name: 'NDJIBU MALU SHAMMAH',
    role: 'Full Stack Developer',
    intro:
      "Je suis une étudiante en Master 1 IMSI et en formation Full Stack Development chez PrimeTek Academy. Passionnée par le développement web et les technologies numériques, j'aime concevoir des interfaces modernes et développer des solutions digitales qui répondent à des besoins réels.",
    primaryBtn: 'Découvrir mes projets',
    secondaryBtn: 'Télécharger mon CV',
    socialTitle: 'Réseaux',
    aboutTitle: 'À propos',
    aboutText:
      'Je suis Ndjibu Malu Shammah, étudiante en Master 1 Ingénierie et Management des Systèmes d’Information. Je développe progressivement mes compétences en développement Full Stack à PrimeTek Academy.\n\nMon intérêt pour les technologies numériques m’amène à explorer la conception d’interfaces web, le développement d’applications et la création de solutions capables de faciliter les activités des entreprises.\n\nJe suis motivée par l’apprentissage continu, la collaboration et la résolution de problèmes à travers la technologie.',
    values: ['Apprentissage continu', 'Créativité & innovation', 'Résolution de problèmes'],
    skillsTitle: 'Compétences techniques',
    skillsGroups: [
      {
        title: 'Front-End Development',
        items: ['HTML5', 'CSS3', 'JavaScript', 'React.js', 'JSX', 'Vue.js', 'Nuxt']
      },
      {
        title: 'React Development',
        items: ['Components', 'Props', 'State Management avec useState', 'Events Handling', 'Forms', 'useEffect']
      },
      {
        title: 'Back-End et gestion des données',
        items: ['JavaScript côté serveur', 'JSON Server', 'Gestion des données JSON', 'Opérations CRUD']
      },
      {
        title: 'Outils et environnement',
        items: ['Visual Studio Code', 'Git', 'GitHub', 'Vite', 'Figma', 'Terminal', 'Node.js']
      }
    ],
    projectsTitle: 'Projets',
    projects: [
      {
        name: 'Quizzy',
        category: 'Interactive Quiz Application',
        description:
          'Quizzy est un projet de développement d’une application interactive de quiz réalisé dans le cadre de ma formation et du travail en équipe chez PrimeTek Academy.',
        role: 'Lead Integrator',
        features: ['Navigation de l’application', 'Expérience interactive', 'Conception centrée utilisateur'],
        tech: ['HTML', 'CSS', 'JavaScript'],
        label: 'Voir le projet'
      },
      {
        name: 'TaskFlow',
        category: 'Task and Project Management Application',
        description:
          'TaskFlow est une application de gestion des tâches et des projets destinée à faciliter l’organisation et le suivi des activités.',
        role: 'Développement collaboratif',
        features: ['Authentification', 'Gestion des utilisateurs', 'Gestion des projets', 'Gestion des tâches', 'Navigation entre pages', 'JSON Server'],
        tech: ['React', 'JavaScript', 'Vite', 'JSON Server', 'CSS'],
        label: 'Voir le projet'
      },
      {
        name: 'SmartResto',
        category: 'Restaurant Management System',
        description:
          'SmartResto est un projet collaboratif de gestion de restaurant développé dans un environnement de travail en équipe.',
        role: 'Catégories et carte du menu',
        features: ['Gestion des catégories', 'Ajout, modification et suppression', 'Ordre d’affichage', 'Nombre de plats par catégorie', 'Recherche des plats disponibles'],
        tech: ['Nuxt', 'Vue.js', 'JavaScript', 'Git', 'GitHub'],
        label: 'Voir le projet'
      }
    ],
    educationTitle: 'Formation',
    education: [
      {
        period: '2024 — Aujourd’hui',
        title: 'Master 1 — Ingénierie et Management des Systèmes d’Information (IMSI)',
        detail: 'Approfondissement des compétences en management et en systèmes d’information.'
      },
      {
        period: '2024 — Aujourd’hui',
        title: 'Full Stack Development — PrimeTek Academy',
        detail: 'Formation pratique centrée sur la création d’applications web modernes et robustes.'
      }
    ],
    contactTitle: 'Travaillons ensemble',
    contactText: 'Je suis ouverte aux opportunités de stages, projets collaboratifs et missions web.',
    contactEmail: 'shammahndjibu@gmail.com',
    contactPhone: '+243 999 393 431',
    footer: '© 2026 Ndjibu Malu Shammah. Tous droits réservés.'
  },
  en: {
    nav: {
      home: 'Home',
      about: 'About',
      skills: 'Skills',
      projects: 'Projects',
      education: 'Education',
      contact: 'Contact'
    },
    badge: 'HELLO, I AM',
    name: 'NDJIBU MALU SHAMMAH',
    role: 'Full Stack Developer',
    intro:
      'I am a Master 1 IMSI student and a Full Stack Development trainee at PrimeTek Academy. Passionate about web development and digital technologies, I enjoy designing modern interfaces and building digital solutions that meet real needs.',
    primaryBtn: 'Discover my projects',
    secondaryBtn: 'Download my CV',
    socialTitle: 'Socials',
    aboutTitle: 'About me',
    aboutText:
      'I am Ndjibu Malu Shammah, a student in Master 1 in Engineering and Management of Information Systems. I am gradually developing my skills in Full Stack development at PrimeTek Academy.\n\nMy interest in digital technologies leads me to explore web interface design, application development, and the creation of solutions that simplify business activities.\n\nI am motivated by continuous learning, collaboration, and problem-solving through technology.',
    values: ['Continuous Learning', 'Creativity & Innovation', 'Problem Solving'],
    skillsTitle: 'Technical skills',
    skillsGroups: [
      {
        title: 'Front-End Development',
        items: ['HTML5', 'CSS3', 'JavaScript', 'React.js', 'JSX', 'Vue.js', 'Nuxt']
      },
      {
        title: 'React Development',
        items: ['Components', 'Props', 'State Management with useState', 'Events Handling', 'Forms', 'useEffect']
      },
      {
        title: 'Back-End and data management',
        items: ['Server-side JavaScript', 'JSON Server', 'JSON data management', 'CRUD operations']
      },
      {
        title: 'Tools and environment',
        items: ['Visual Studio Code', 'Git', 'GitHub', 'Vite', 'Figma', 'Terminal', 'Node.js']
      }
    ],
    projectsTitle: 'Projects',
    projects: [
      {
        name: 'Quizzy',
        category: 'Interactive Quiz Application',
        description:
          'Quizzy is a quiz application project developed as part of my training and teamwork at PrimeTek Academy.',
        role: 'Lead Integrator',
        features: ['App navigation', 'Interactive experience', 'User-centered design'],
        tech: ['HTML', 'CSS', 'JavaScript'],
        label: 'View project'
      },
      {
        name: 'TaskFlow',
        category: 'Task and Project Management Application',
        description:
          'TaskFlow is a task and project management application designed to facilitate organization and tracking of activities.',
        role: 'Collaborative development',
        features: ['Authentication', 'User management', 'Project management', 'Task management', 'Page navigation', 'JSON Server'],
        tech: ['React', 'JavaScript', 'Vite', 'JSON Server', 'CSS'],
        label: 'View project'
      },
      {
        name: 'SmartResto',
        category: 'Restaurant Management System',
        description:
          'SmartResto is a collaborative restaurant management project developed in a team environment.',
        role: 'Categories and menu board',
        features: ['Category management', 'Create, edit, delete categories', 'Display order', 'Dishes count by category', 'Dish search'],
        tech: ['Nuxt', 'Vue.js', 'JavaScript', 'Git', 'GitHub'],
        label: 'View project'
      }
    ],
    educationTitle: 'Education & training',
    education: [
      {
        period: '2024 — Present',
        title: 'Master 1 — Engineering and Management of Information Systems (IMSI)',
        detail: 'Deepening of skills in management and information systems.'
      },
      {
        period: '2024 — Present',
        title: 'Full Stack Development — PrimeTek Academy',
        detail: 'Hands-on training focused on modern, robust web application development.'
      }
    ],
    contactTitle: 'Let’s work together',
    contactText: 'I am open to internships, collaborative projects, and web missions.',
    contactEmail: 'shammahndjibu@gmail.com',
    contactPhone: '+243 999 393 431',
    footer: '© 2026 Ndjibu Malu Shammah. All rights reserved.'
  }
} as const

const t = computed(() => locale[currentLanguage.value])

const navItems = computed(() => [
  { id: 'home', label: t.value.nav.home },
  { id: 'about', label: t.value.nav.about },
  { id: 'skills', label: t.value.nav.skills },
  { id: 'projects', label: t.value.nav.projects },
  { id: 'education', label: t.value.nav.education },
  { id: 'contact', label: t.value.nav.contact }
])

const applyTheme = () => {
  if (typeof document !== 'undefined') {
    document.documentElement.classList.toggle('dark', currentTheme.value === 'dark')
  }
}

watch(currentTheme, () => {
  applyTheme()
}, { immediate: true })

onMounted(() => {
  applyTheme()
})

const toggleTheme = () => {
  currentTheme.value = currentTheme.value === 'light' ? 'dark' : 'light'
}

const toggleLanguage = () => {
  currentLanguage.value = currentLanguage.value === 'fr' ? 'en' : 'fr'
}
</script>

<template>
  <main class="portfolio-page">
    <header class="topbar">
      <div class="container nav-shell">
        <a href="#home" class="brand" aria-label="Accueil">
          SHAMMAH
        </a>

        <button
          class="nav-toggle"
          type="button"
          aria-label="Open navigation"
          @click="menuOpen = !menuOpen"
        >
          <span />
          <span />
          <span />
        </button>

        <nav :class="['nav-links', { open: menuOpen }]" aria-label="Main navigation">
          <a v-for="item in navItems" :key="item.id" :href="`#${item.id}`" @click="menuOpen = false">
            {{ item.label }}
          </a>
        </nav>

        <div class="nav-actions">
          <button class="lang-switch" type="button" @click="toggleLanguage">
            {{ currentLanguage === 'fr' ? 'EN' : 'FR' }}
          </button>

          <button class="theme-switch" type="button" @click="toggleTheme" :aria-label="currentTheme === 'light' ? 'Switch to dark mode' : 'Switch to light mode'">
            {{ currentTheme === 'light' ? '☾' : '☀' }}
          </button>
        </div>
      </div>
    </header>

    <section id="home" class="hero">
      <div class="container hero-grid">
        <div class="hero-copy">
          <span class="eyebrow">{{ t.badge }}</span>
          <h1>{{ t.name }}</h1>
          <div class="title-row">
            <span class="title-pill">{{ t.role }}</span>
          </div>

          <p class="lead">
            {{ t.intro }}
          </p>

          <div class="cta-group">
            <a href="#projects" class="primary-btn">{{ t.primaryBtn }}</a>
            <a href="/cv.pdf" download class="secondary-btn">{{ t.secondaryBtn }}</a>
          </div>

          <div class="socials">
            <span>{{ t.socialTitle }}</span>
            <div class="social-links">
              <a href="https://github.com/shammah-lab" target="_blank" rel="noreferrer">GitHub</a>
              <a href="https://linkedin.com/in/shammah-ndjibu-01b685309" target="_blank" rel="noreferrer">LinkedIn</a>
              <a :href="`mailto:${t.contactEmail}`">Email</a>
            </div>
          </div>
        </div>

        <div class="hero-visual" aria-label="Profile artwork">
          <div class="portrait-card">
            <div class="portrait-frame">
              <div class="portrait-figure">
                <img src="/images/shammah.jpg" alt="Ndjibu Malu Shammah portrait" />
              </div>
            </div>
          </div>

          <div class="floating-card card-one">
            <small>Focus</small>
            <strong>UI / UX</strong>
          </div>

          <div class="floating-card card-two">
            <small>Stack</small>
            <strong>Nuxt + Vue</strong>
          </div>
        </div>
      </div>
    </section>

    <section id="about" class="section">
      <div class="container section-header">
        <span class="section-kicker">{{ t.aboutTitle }}</span>
        <h2>{{ t.aboutTitle }}</h2>
      </div>

      <div class="container about-grid">
        <div class="about-copy">
          <p>{{ t.aboutText }}</p>
        </div>

        <div class="values-panel">
          <div v-for="value in t.values" :key="value" class="value-card">
            <span class="value-dot" aria-hidden="true" />
            <span>{{ value }}</span>
          </div>
        </div>
      </div>
    </section>

    <section id="skills" class="section muted-section">
      <div class="container section-header">
        <span class="section-kicker">{{ t.skillsTitle }}</span>
        <h2>{{ t.skillsTitle }}</h2>
      </div>

      <div class="container skills-grid">
        <article v-for="group in t.skillsGroups" :key="group.title" class="skill-card">
          <h3>{{ group.title }}</h3>
          <ul>
            <li v-for="item in group.items" :key="item">{{ item }}</li>
          </ul>
        </article>
      </div>
    </section>

    <section id="projects" class="section">
      <div class="container section-header">
        <span class="section-kicker">{{ t.projectsTitle }}</span>
        <h2>{{ t.projectsTitle }}</h2>
      </div>

      <div class="container project-grid">
        <article v-for="project in t.projects" :key="project.name" class="project-card">
          <div class="project-visual">
            <div class="project-thumb">
              <span>{{ project.name.slice(0, 2).toUpperCase() }}</span>
            </div>
          </div>

          <div class="project-body">
            <div class="project-meta">
              <span>{{ project.category }}</span>
            </div>
            <h3>{{ project.name }}</h3>
            <p>{{ project.description }}</p>

            <div class="project-row">
              <strong>Rôle</strong>
              <span>{{ project.role }}</span>
            </div>

            <div class="project-row">
              <strong>Fonctionnalités</strong>
              <span>{{ project.features.join(' • ') }}</span>
            </div>

            <div class="tag-list">
              <span v-for="tech in project.tech" :key="tech">{{ tech }}</span>
            </div>

            <div class="project-actions">
              <a href="#contact" class="primary-btn small">{{ project.label }}</a>
              <a href="#contact" class="secondary-btn small">Code</a>
            </div>
          </div>
        </article>
      </div>
    </section>

    <section id="education" class="section muted-section">
      <div class="container section-header">
        <span class="section-kicker">{{ t.educationTitle }}</span>
        <h2>{{ t.educationTitle }}</h2>
      </div>

      <div class="container timeline">
        <article v-for="item in t.education" :key="item.title" class="timeline-item">
          <div class="timeline-dot" aria-hidden="true" />
          <div class="timeline-content">
            <span class="timeline-period">{{ item.period }}</span>
            <h3>{{ item.title }}</h3>
            <p>{{ item.detail }}</p>
          </div>
        </article>
      </div>
    </section>

    <section id="contact" class="section contact-section">
      <div class="container contact-panel">
        <div>
          <span class="section-kicker">{{ t.nav.contact }}</span>
          <h2>{{ t.contactTitle }}</h2>
        </div>

        <p>{{ t.contactText }}</p>

        <div class="contact-actions">
          <a :href="`mailto:${t.contactEmail}`" class="primary-btn">{{ t.contactEmail }}</a>
          <a :href="`tel:${t.contactPhone}`" class="secondary-btn">{{ t.contactPhone }}</a>
          <a href="https://linkedin.com/in/shammah-ndjibu-01b685309" target="_blank" rel="noreferrer" class="secondary-btn">LinkedIn</a>
          <a href="https://github.com/shammah-lab" target="_blank" rel="noreferrer" class="secondary-btn">GitHub</a>
        </div>
      </div>
    </section>

    <footer class="site-footer">
      <div class="container footer-shell">
        <p>{{ t.footer }}</p>
      </div>
    </footer>
  </main>
</template>
