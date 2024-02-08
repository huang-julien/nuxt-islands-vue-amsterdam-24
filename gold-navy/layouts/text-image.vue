<template>
    <div class="slidev-layout">
      <div
        class="flex h-full"
        :class="$attrs.reverse ? 'gap-16' : 'gap-8'"
      >
        <div
          class="pr-16 flex flex-col"
          :class="[{ 'order-1': $attrs.reverse }, contentWrapperClass]"
        >
          <slot  />
        </div>
        <figure class="relative flex flex-col justify-center" :class="imgWrapperClass">
          <img
            :src="media"
            class="rounded-lg shadow-lg object-cover z-10"
            :class="imgClass"
          >
          <figcaption class="mt-2 text-xs w-full">
            {{ $attrs.caption }}
          </figcaption>
        </figure>
      </div>
    </div>
  </template>

<script setup lang="ts">
import { computed } from 'vue';

const props = defineProps<{
    reversed?: boolean
    media: string
    imgClass: string
    contentWrapperClass: string
    imgWrapperClass: string
}>()

const classes = computed(() => ([{
    'flex-reverse': props.reversed,

}, ]))
</script>

<style lang="scss">
</style>