<template>
    <section id="home" class="relative min-h-screen flex items-center justify-center overflow-hidden">
        <!-- Background Image with Overlay -->
        <div class="absolute inset-0">
            <div class="absolute inset-0 bg-gradient-to-br from-gray-900 via-primary-900 to-secondary-900"></div>
            <div class="absolute inset-0 bg-black/30"></div>
            <!-- Background pattern -->
            <div class="absolute inset-0 opacity-10">
                <svg class="w-full h-full" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100">
                    <pattern id="grid" width="10" height="10" patternUnits="userSpaceOnUse">
                        <path d="M 10 0 L 0 0 0 10" fill="none" stroke="white" stroke-width="0.5" />
                    </pattern>
                    <rect width="100" height="100" fill="url(#grid)" />
                </svg>
            </div>
        </div>

        <!-- Mountain Silhouette -->
        <div class="absolute bottom-0 left-0 right-0">
            <svg viewBox="0 0 1200 320" class="w-full h-auto text-black/30">
                <path fill="currentColor"
                    d="M0,320L80,300C160,280,320,240,480,213.3C640,187,800,173,960,186.7C1120,200,1280,240,1360,260L1440,280L1440,320L1360,320C1280,320,1120,320,960,320C800,320,640,320,480,320C320,320,160,320,80,320L0,320Z">
                </path>
            </svg>
        </div>

        <!-- Content -->
        <div class="relative z-10 text-center px-4 sm:px-6 lg:px-8 max-w-5xl mx-auto">
            <!-- Main Heading -->
            <div class="my-[20px]">
                <h1
                    class="text-5xl sm:text-5xl md:text-5xl lg:text-8xl font-black text-white leading-none tracking-wider">
                    <span class="block">Software </span>
                    <span
                        class="block text-transparent bg-clip-text bg-gradient-to-r from-primary-500 via-secondary-500 to-primary-400">
                        Engineer
                    </span>
                </h1>
            </div>

            <!-- Description -->
            <div class="mb-12 max-w-2xl mx-auto">
                <p class="text-lg sm:text-xl text-gray-200 mb-2">
                    {{ branding.hero.description.intro }}
                </p>
            </div>

            <!-- CTA Button -->
            <div class="flex justify-center">
                <BaseButton variant="primary" size="lg" :show-arrow="true" @click="scrollToContact">
                    {{ branding.hero.cta }}
                </BaseButton>
            </div>

            <!-- Scroll Indicator -->
            <div class="absolute bottom-8 left-1/2 transform -translate-x-1/2">
                <div class="animate-bounce">
                    <svg class="w-6 h-6 text-white/70" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="M19 14l-7 7m0 0l-7-7m7 7V3"></path>
                    </svg>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import BaseButton from './BaseButton.vue'

const props = defineProps({
    branding: {
        type: Object,
        required: true
    }
})

const scrollToContact = () => {
    const contactSection = document.querySelector('#contact')
    if (contactSection) {
        contactSection.scrollIntoView({ behavior: 'smooth' })
    }
}
</script>

<style scoped>
/* Add some glow effects */
.text-transparent {
    text-shadow: 0 0 30px rgba(217, 42, 42, 0.5);
}

/* Subtle animation for the background */
@keyframes float {

    0%,
    100% {
        transform: translateY(0px) rotate(0deg);
    }

    50% {
        transform: translateY(-10px) rotate(1deg);
    }
}

.animate-float {
    animation: float 6s ease-in-out infinite;
}
</style>
