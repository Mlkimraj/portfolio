<template>
    <nav
        class="fixed top-0 left-0 right-0 z-50 bg-gradient-to-r from-gray-900/90 via-primary-900/90 to-secondary-900/90 backdrop-blur-md border-b border-primary-700/30">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-16">
                <!-- Logo -->
                <div class="flex-shrink-0">
                    <div class="px-4 py-2 bg-white/10 backdrop-blur-sm rounded-lg flex items-center justify-center border border-white/20">
                        <span class="text-white font-bold text-lg tracking-wide">{{ branding.logo }}</span>
                    </div>
                </div>

                <!-- Desktop Navigation -->
                <div class="hidden md:block">
                    <div class="ml-10 flex items-baseline space-x-8">
                        <a v-for="item in props.navItems" :key="item.name" :href="item.href"
                            class="text-white hover:text-gray-300 px-3 py-2 text-sm font-medium transition-colors duration-200"
                            :class="{ 'border-b-2 border-white': item.active }"
                            @click="handleNavClick(item.name)">
                            {{ item.name }}
                        </a>
                    </div>
                </div>

                <!-- Social Links -->
                <SocialLinks />

                <!-- Mobile menu button -->
                <div class="md:hidden">
                    <button @click="mobileMenuOpen = !mobileMenuOpen"
                        class="text-white hover:text-gray-300 focus:outline-none focus:text-gray-300">
                        <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path v-if="!mobileMenuOpen" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                d="M4 6h16M4 12h16M4 18h16" />
                            <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                d="M6 18L18 6M6 6l12 12" />
                        </svg>
                    </button>
                </div>
            </div>
        </div>

        <!-- Mobile menu -->
        <div v-if="mobileMenuOpen" class="md:hidden">
            <div
                class="px-2 pt-2 pb-3 space-y-1 bg-gradient-to-r from-gray-900/95 via-primary-900/95 to-secondary-900/95 backdrop-blur-md">
                <a v-for="item in props.navItems" :key="item.name" :href="item.href"
                    class="text-white hover:text-gray-300 block px-3 py-2 text-base font-medium"
                    @click="handleNavClick(item.name); mobileMenuOpen = false">
                    {{ item.name }}
                </a>
            </div>
        </div>
    </nav>
</template>

<script setup>
import { ref } from 'vue'
import SocialLinks from './SocialLinks.vue'

const props = defineProps({
    navItems: {
        type: Array,
        required: true
    },
    branding: {
        type: Object,
        required: true
    }
})

const emit = defineEmits(['nav-click'])

const mobileMenuOpen = ref(false)

const handleNavClick = (itemName) => {
    emit('nav-click', itemName)
}
</script>
