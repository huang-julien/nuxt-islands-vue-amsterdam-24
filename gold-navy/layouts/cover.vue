<template>
  <div class="slidev-layout cover grid">
    <div class="my-auto">
      <slot />
    </div>
  </div>
</template>

<style lang="scss">
.slidev-layout.cover {
  font-weight: bold;
  h1 {
    font-size: 2.5em;
  }
}
</style>