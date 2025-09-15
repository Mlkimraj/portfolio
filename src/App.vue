<template>
  <div class="min-h-screen bg-gradient-to-br from-gray-900 via-primary-900 to-secondary-900">
    <!-- Navigation -->
    <TheNavbar :nav-items="navItems" :branding="branding" @nav-click="handleNavClick" />

    <!-- Main Content -->
    <main>
      <!-- Hero Section -->
      <HeroSection :branding="branding" />

      <!-- Client Testimonials Section -->
      <ClientTestimonials :testimonials="testimonials" :stats="stats" :branding="branding" />

      <!-- Projects Section -->
      <ProjectsSection :projects="projects" :branding="branding" />

      <section id="contact"
        class="relative py-[10px] bg-gradient-to-br from-gray-900 via-primary-900 to-secondary-900 overflow-hidden min-h-screen flex flex-col justify-between">
        <GradientSection />
        <Footer :nav-items="footerNavItems" :branding="branding" />
      </section>
    </main>

  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import TheNavbar from './components/TheNavbar.vue'
import HeroSection from './components/HeroSection.vue'
import ClientTestimonials from './components/ClientTestimonials.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import Footer from './components/Footer.vue'

// Import constants
import { navItems as staticNavItems, footerNavItems } from './constants/navigation.js'
import { projects } from './constants/projects.js'
import { testimonials, stats } from './constants/testimonials.js'
import { branding } from './constants/branding.js'
import GradientSection from './components/GradientSection.vue'

// Create reactive navigation items
const navItems = ref([...staticNavItems])

// Function to handle navigation item clicks
const handleNavClick = (clickedItemName) => {
  navItems.value.forEach(item => {
    item.active = item.name === clickedItemName
  })
}

// Function to update navigation based on current section
const updateNavigation = (sectionId) => {
  const sectionToNavMap = {
    'home': 'Home',
    'reviews': 'Reviews', 
    'projects': 'Projects',
    'contact': 'Contact'
  }
  
  const activeNavName = sectionToNavMap[sectionId]
  if (activeNavName) {
    navItems.value.forEach(item => {
      item.active = item.name === activeNavName
    })
  }
}

// Intersection Observer for scroll detection
let observer = null

onMounted(() => {
  // Wait for DOM to be fully rendered
  setTimeout(() => {
    let visibleSections = new Map()
    
    // Create intersection observer
    observer = new IntersectionObserver(
      (entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            visibleSections.set(entry.target.id, entry.intersectionRatio)
            console.log(`Section ${entry.target.id} is intersecting with ratio: ${entry.intersectionRatio}`)
          } else {
            visibleSections.delete(entry.target.id)
          }
        })
        
        // Find the section with the highest intersection ratio
        if (visibleSections.size > 0) {
          let mostVisibleSection = ''
          let highestRatio = 0
          
          for (const [sectionId, ratio] of visibleSections) {
            if (ratio > highestRatio) {
              highestRatio = ratio
              mostVisibleSection = sectionId
            }
          }
          
          if (mostVisibleSection) {
            updateNavigation(mostVisibleSection)
          }
        }
      },
      {
        threshold: [0, 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9, 1.0], // Multiple thresholds for better detection
        rootMargin: '-80px 0px -80px 0px' // Account for fixed navbar height
      }
    )

    // Observe all sections
    const sections = ['home', 'reviews', 'projects', 'contact']
    sections.forEach(sectionId => {
      const section = document.getElementById(sectionId)
      if (section) {
        console.log(`Observing section: ${sectionId}`)
        observer.observe(section)
      } else {
        console.warn(`Section with id "${sectionId}" not found`)
      }
    })
  }, 100)
})

onUnmounted(() => {
  if (observer) {
    observer.disconnect()
  }
})
</script>

<style>
/* Smooth scrolling */
html {
  scroll-behavior: smooth;
}

/* Remove default margins */
body {
  margin: 0;
  padding: 0;
}
</style>