<template>
  <div class="min-h-screen bg-gradient-to-br from-gray-900 via-primary-900 to-secondary-900">
    <!-- Navigation -->
    <TheNavbar :nav-items="navItems" :branding="branding" />

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
import TheNavbar from './components/TheNavbar.vue'
import HeroSection from './components/HeroSection.vue'
import ClientTestimonials from './components/ClientTestimonials.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import Footer from './components/Footer.vue'

// Import constants
import { navItems, footerNavItems } from './constants/navigation.js'
import { projects } from './constants/projects.js'
import { testimonials, stats } from './constants/testimonials.js'
import { branding } from './constants/branding.js'
import GradientSection from './components/GradientSection.vue'
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