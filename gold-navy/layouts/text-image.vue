<template>
    <div class="slidev-layout text-image">
        <div class="flex w-full" :class="classes">
            <div>

                <slot />
            </div>
            <div class="p-5">
                <img :src="imgUrl" class="rounded-full border-solid border-" />
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
import { computed } from 'vue';

const props = defineProps<{
    reversed?: boolean
    imgUrl: string
}>()

const classes = computed(() => ([{
    'flex-reverse': props.reversed,

}, ]))
</script>

<style lang="scss">
</style>