<template>
    <section id="projects"
        class="relative py-20 bg-gradient-to-br from-gray-900 via-primary-900 to-secondary-900 overflow-hidden">
        <!-- Background decoration -->
        <div class="absolute inset-0 bg-black/40"></div>
        <div class="absolute inset-0 bg-gradient-to-r from-primary-800/20 via-gray-800/10 to-secondary-800/20"></div>

        <div class="relative max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <!-- Header -->
            <SectionTitle :title="branding.sections.projects.title" />

            <!-- Projects Grid -->
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <div v-for="(project, index) in props.projects" :key="index"
                    class="group bg-primary-900/60 backdrop-blur-sm cursor-pointer rounded-3xl p-8 hover:bg-primary-800/70 transition-all duration-300 transform hover:-translate-y-2 shadow-2xl hover:shadow-primary-500/30 border border-gray-700/30">
                    <!-- Large Project Image -->
                    <div class="relative mb-8">
                        <div
                            class="relative w-full h-48 rounded-2xl overflow-hidden bg-gradient-to-br from-primary-600 via-secondary-600 to-primary-700">
                            <img :src="project.images[0]" :alt="`${project.name} preview`"
                                class="w-full h-full object-cover opacity-90" />
                            <!-- Image Overlay -->
                            <div class="absolute inset-0 bg-gradient-to-t from-black/60 via-transparent to-transparent">
                            </div>
                        </div>
                    </div>

                    <!-- Project Title -->
                    <h3 class="text-left text-white font-bold text-3xl mb-4">{{ project.name }}</h3>

                    <!-- Project URL -->
                    <div class="text-left mb-6">
                        <a :href="project.url" target="_blank" rel="noopener noreferrer"
                            class="text-secondary-400 hover:text-secondary-300 transition-colors duration-200 text-base font-medium underline">
                            {{ project.url }}
                        </a>
                    </div>

                    <!-- Project Description -->
                    <div class="mb-10 space-y-3 text-left">
                        <p v-for="(desc, descIndex) in project.description" :key="descIndex"
                            class="text-gray-300 text-base leading-relaxed flex items-start">
                            <span class="text-gray-400 mr-3 mt-1">•</span>
                            <span>{{ desc }}</span>
                        </p>
                    </div>

                    <!-- Tech Stack Icons -->
                    <div class="flex items-center justify-start space-x-4">
                        <div v-for="(tech, techIndex) in project.techStack" :key="techIndex" :class="[
                            'w-12 h-12 rounded-xl flex items-center justify-center text-white font-bold text-sm transition-transform duration-200 hover:scale-105 shadow-lg',
                            tech.color
                        ]" :title="tech.name">
                            <img v-if="tech.iconImage" :src="tech.iconImage" :alt="tech.name"
                                class="w-8 h-8 object-contain" />
                            <span v-else>{{ tech.icon }}</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import SectionTitle from './SectionTitle.vue'

const props = defineProps({
    projects: {
        type: Array,
        required: true
    },
    branding: {
        type: Object,
        required: true
    }
})
</script>

<style scoped>
/* Smooth background transition */
.bg-gradient-to-br {
    animation: gradientShift 12s ease-in-out infinite alternate;
}

@keyframes gradientShift {
    0% {
        background-position: 0% 50%;
    }

    100% {
        background-position: 100% 50%;
    }
}

/* Hover effects for project cards */
.group:hover {
    transform: translateY(-8px);
}

/* Tech stack icon hover effects */
.group:hover [title] {
    transform: scale(1.1);
}
</style>
