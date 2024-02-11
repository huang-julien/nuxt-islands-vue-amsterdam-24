
 <template>
    <div class="slidev-layout with-title">
        <TitleOverlay v-click-hide>
            <slot v-if="$slots.title" name="title" />
            <template v-else>
                <h1 class="text-5xl font-bold text-gold">{{ title }}</h1>
            </template>
        </TitleOverlay>

        <slot />
    </div>
</template>

<script setup lang="ts">
defineProps<{
    title?: string
}>()
</script>