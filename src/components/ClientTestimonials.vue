<template>
    <section id="reviews"
        class="relative py-20 bg-gradient-to-br from-gray-900 via-primary-900 to-secondary-900 overflow-hidden">
        <!-- Background decoration -->
        <div class="absolute inset-0 bg-black/40"></div>
        <div class="absolute inset-0 bg-gradient-to-r from-primary-800/20 via-gray-800/10 to-secondary-800/20"></div>

        <div class="relative max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <!-- Header -->
            <SectionTitle :title="branding.sections.testimonials.title"
                :highlight="branding.sections.testimonials.highlight"
                :subtitle="branding.sections.testimonials.subtitle" />

            <!-- Stats Pills -->
            <div class="flex flex-wrap items-center justify-center gap-4 my-5">
                <div v-for="(stat, index) in props.stats" :key="index"
                    class="bg-gray-900/50 border border-gray-700 rounded-full px-6 py-3">
                    <span :class="stat.color + ' font-semibold'">{{ stat.label }}</span>
                </div>
            </div>

            <!-- Moving Testimonials Slider -->
            <div class="relative overflow-hidden">
                <div class="flex animate-scroll space-x-6">
                    <div v-for="(testimonial, index) in duplicatedTestimonials" :key="index"
                        class="flex-shrink-0 w-80 bg-gray-900/50 backdrop-blur-sm border border-gray-800 rounded-2xl p-6 hover:border-gray-600 transition-all duration-300">
                        <div class="flex items-center space-x-3 mb-4">
                            <img :src="testimonial.avatar" :alt="testimonial.name"
                                class="w-12 h-12 rounded-full object-cover" />
                            <div>
                                <h4 class="font-semibold text-white">{{ testimonial.name }}</h4>
                                <p class="text-gray-400 text-sm">{{ testimonial.handle }}</p>
                            </div>
                        </div>
                        <p class="text-gray-300 leading-relaxed">{{ testimonial.text }}</p>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import { computed } from 'vue'
import SectionTitle from './SectionTitle.vue'

const props = defineProps({
    testimonials: {
        type: Array,
        required: true
    },
    stats: {
        type: Array,
        required: true
    },
    branding: {
        type: Object,
        required: true
    }
})

// Duplicate testimonials for seamless loop
const duplicatedTestimonials = computed(() => [...props.testimonials, ...props.testimonials])
</script>

<style scoped>
@keyframes scroll {
    0% {
        transform: translateX(0);
    }

    100% {
        transform: translateX(-50%);
    }
}

.animate-scroll {
    animation: scroll 30s linear infinite;
}

.animate-scroll:hover {
    animation-play-state: paused;
}

/* Smooth background transition */
.bg-gradient-to-br {
    animation: gradientShift 8s ease-in-out infinite alternate;
}

@keyframes gradientShift {
    0% {
        background-position: 0% 50%;
    }

    100% {
        background-position: 100% 50%;
    }
}
</style>
