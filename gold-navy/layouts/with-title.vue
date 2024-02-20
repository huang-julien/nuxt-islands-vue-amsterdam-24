
 <template>
    <div class="slidev-layout with-title">
        <Transition name="fade">
            <TitleOverlay v-click-hide>
                <slot v-if="$slots.title" name="title" />
                <template v-else>
                    <h1 class="text-5xl font-bold text-gold">{{ title }}</h1>
                </template>
            </TitleOverlay>
        </Transition>
        

        <slot />
    </div>
</template>

<script setup lang="ts">
defineProps<{
    title?: string
}>()
</script>