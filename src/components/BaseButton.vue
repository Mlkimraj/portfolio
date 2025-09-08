<template>
    <button :class="buttonClasses" @click="$emit('click')">
        <slot />
        <svg v-if="showArrow" class="w-4 h-4 ml-2 transition-transform group-hover:translate-x-1" fill="none"
            stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3" />
        </svg>
    </button>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
    variant: {
        type: String,
        default: 'primary',
        validator: (value) => ['primary', 'secondary', 'outline'].includes(value)
    },
    size: {
        type: String,
        default: 'md',
        validator: (value) => ['sm', 'md', 'lg'].includes(value)
    },
    showArrow: {
        type: Boolean,
        default: false
    }
})

defineEmits(['click'])

const buttonClasses = computed(() => {
    const baseClasses = 'group inline-flex items-center justify-center font-medium transition-all duration-200 focus:outline-none focus:ring-2 focus:ring-offset-2'

    const variants = {
        primary: 'bg-gradient-to-r from-primary-500 to-secondary-500 text-white hover:from-primary-600 hover:to-secondary-600 focus:ring-primary-500',
        secondary: 'bg-transparent text-white border-2 border-primary-500 hover:bg-primary-500 hover:text-white focus:ring-primary-500',
        outline: 'bg-transparent text-white border border-primary-500/50 hover:border-primary-500 hover:bg-primary-500/10 focus:ring-primary-500'
    }

    const sizes = {
        sm: 'px-4 py-2 text-sm rounded-md',
        md: 'px-6 py-3 text-base rounded-lg',
        lg: 'px-8 py-4 text-lg rounded-xl'
    }

    return [
        baseClasses,
        variants[props.variant],
        sizes[props.size]
    ].join(' ')
})
</script>
