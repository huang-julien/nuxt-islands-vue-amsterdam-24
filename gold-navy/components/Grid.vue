<template>
    <div class="grid" :class="classes">
        <slot />
    </div>
</template>

<script setup lang="ts">
import {computed} from "vue"
const props = withDefaults(defineProps<{
    cols: number
}>(), {
    cols: 2
})

const classes = computed(() => (`grid-cols-${props.cols}`))
</script>