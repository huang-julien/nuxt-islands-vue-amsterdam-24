<template>
  <div class="window border flex flex-col border-solid border-slate-700 bg-dark-blue text-white rounded-md relative">
    <div class="flex py-1 px-2">
      <div class="text-[0.6rem]">{{ filename }}</div>
      <div class="grid grid-cols-3 gap-1 ml-auto">
        <div class="rounded-full w-3 h-3 bg-red-400 inline-block" />
        <div class="rounded-full w-3 h-3 bg-yellow-300 inline-block" />
        <div class="rounded-full w-3 h-3 bg-green-500 inline-block" />
      </div>
    </div>
    <div class="text-xs flex-1">
      <slot />
    </div>
  </div>
</template>

<script setup lang="ts">
defineProps<{
  filename?: string
}>()
</script>

<style>
.window div.slidev-code-wrapper {
  height: 100%;
}
.window .shiki {
  height: 100%;
  overflow: auto;
}
</style>