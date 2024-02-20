<template>
    <footer class="mt-auto flex">
        <img v-if="leftLogo" :class="leftLogoClass" :src="leftLogo" alt="footer logo" />
        <div v-if="twitter" class="ml-auto">
            <logos-twitter /> {{ twitter }}
        </div>
    </footer>
</template>

<script setup lang="ts">    

defineProps<{
    twitter?: string,
    leftLogo?: string,
    leftLogoClass?: string
}>()
</script>
