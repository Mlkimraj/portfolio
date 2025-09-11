<script setup>
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
</script>

<template>
    <div class="relative">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div
                class="flex flex-col lg:flex-row justify-between items-start lg:items-end space-y-8 lg:space-y-0 border-t border-primary-500 pt-8">
                <!-- Left Side - Brand and Navigation -->
                <div class="flex flex-col space-y-6">
                    <h3 class="text-3xl font-bold text-white">{{ branding.footerTitle }}</h3>
                    <nav class="flex flex-wrap gap-8">
                        <a v-for="item in props.navItems" :key="item.name" :href="item.href"
                            class="text-white/80 hover:text-white transition-colors duration-200 text-lg font-medium">
                            {{ item.name }}
                        </a>
                    </nav>
                </div>

                <!-- Right Side - Social Links and Copyright -->
                <div class="flex flex-col items-start lg:items-end space-y-6">
                    <!-- Social Icons -->
                    <div class="flex items-center space-x-5">
                        <!-- Social Links -->
                        <SocialLinks />
                    </div>

                    <p class="text-white/70 text-lg font-medium">{{ branding.copyright }}</p>
                </div>
            </div>
        </div>
    </div>
</template>