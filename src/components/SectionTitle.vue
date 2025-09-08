<template>
    <div class="text-center">
        <h2 :class="[
            'font-bold mb-6',
            textColor,
            titleSize
        ]">
            {{ title }}
            <span v-if="highlight" class="bg-gradient-to-r from-primary-400 to-secondary-500 bg-clip-text text-transparent">
                {{ highlight }}
            </span>
        </h2>
        <p v-if="subtitle" :class="[
            'leading-relaxed max-w-3xl mx-auto',
            subtitleColor,
            subtitleSize
        ]">
            {{ subtitle }}
        </p>
    </div>
</template>

<script setup>
// Define props for customization
const props = defineProps({
    // Main title text (required)
    title: {
        type: String,
        required: true
    },

    // Optional highlighted text that appears after the title
    highlight: {
        type: String,
        default: ''
    },

    // Optional subtitle/description
    subtitle: {
        type: String,
        default: ''
    },

    // Title text color classes
    textColor: {
        type: String,
        default: 'text-white'
    },

    // Title size classes
    titleSize: {
        type: String,
        default: 'text-4xl md:text-5xl'
    },

    // Subtitle text color classes
    subtitleColor: {
        type: String,
        default: 'text-gray-300'
    },

    // Subtitle size classes
    subtitleSize: {
        type: String,
        default: 'text-lg md:text-xl'
    }
})
</script>