<template>
    <div class="badge rounded-lg border border-solid inline px-1" :class="type">
        <slot />
    </div>
</template>

<script setup lang="ts">
defineProps<{
    type: 'error' | 'warning' | 'success' | 'info'
}>()
</script>

<style lang="scss">
.badge {
    &.error {
        @apply bg-red-500 text-white bg-opacity-50 border-red-500;
    }
    &.info {
        @apply bg-blue-500 text-white bg-opacity-50 border-blue-500;
    }
    &.warning {
        @apply bg-yellow-500 text-white bg-opacity-50 border-yellow-500;
    }
    &.success {
        @apply bg-green-500 text-white bg-opacity-50 border-green-500;
    }
}
</style>