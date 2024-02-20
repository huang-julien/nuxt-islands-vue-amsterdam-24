---
theme: ./gold-navy
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
drawings:
  persist: false
title: Welcome to Slidev
mdc: true
transition: fade
layout: intro
---

<img src="/assets/island_scene.svg" class="absolute z-10 bottom-0 top-20 left-10 right-10" >
 
# Ship less javascript with NuxtIsland
 

---
layout: text-image
media: https://avatars.githubusercontent.com/u/63512348?v=4
content-wrapper-class: w-3/4
img-class: "!rounded-full border-4 border-solid border-gold"
---

# Julien Huang
 
- ### Frontend developer at <LeetchiLogo class="h-6 text-[#f7c0b9] mb-1 inline" />
- ### Open-source enthusiast
- ### <ri-team-fill /> Nuxt Core team member <logos-nuxt-icon />

<div class="mt-15" />

Other hobbies
- Playing A LOT of video games <emojione-v1-keyboard-and-mouse />
- Practicing flute and piano <material-symbols-music-note/> 
- working out <guidance-weightlifting/>

---
layout: with-title
title: Story about server components
---

# Before single page application

- <mdi-server />  Everything was rendered by the server
- <ph-link-bold /> Very tight relationship between frontend and backend

---
layout: text-image
media: /assets/frameworks-everywhere.jpg
imgWrapperClass: w-1/2
---

::title::

# Rise of frontend frameworks

::default::

- Untied frontend from backend
- Frontend become much more flexible
- Great level of interactivity

<div class="mt-5" />

- Everything was pushed client-side

---
layout: text-image
media: /assets/the_rising_of_metaframeworks.jpg
imgWrapperClass: w-1/2
reverse: true
---

::title::

# The rising of meta-frameworks

::default::

- re-couple frontend and backend
- higher level, brings another layer of abstraction for developers

<div class="mt-5" />

- Applications are becoming even more complex

---
layout: with-title
title: Hydration
---

# What is it ?

Hydration is the process by which frameworks initialize an application on top of server-rendered HTML.


<img src="/assets/finally.jpg" class="w-1/2 mx-auto rounded-xl" />

---

# How does it work ?

<img src="/assets/hydration-flow.png" class="rounded-xl mt-20" >

---

# Here comes server only components

- rendered only server-side
- sent in a format that will be read by the framework or a by a custom component
- render the result as static HTML
- non-interactive by default

---

# Some example of Island and server components

<div grid-cols-3 flex justify-around text-3xl mt-50>
<div flex flex-col>
<skill-icons-react-dark mx-auto  />
<p>RSC</p>
</div>
<div flex flex-col >
<skill-icons-nuxtjs-dark  mx-auto />
<p>NuxtIslands</p>
</div>
<div flex flex-col>
<skill-icons-astro  mx-auto />
<p>Astro Islands</p>
</div>

</div>

---
layout: with-title
title: Benefits
---

# Safely write server code within your component 

- only run server-side
- safe access to private configuration without risking leaks

::window

```vue
<template>
 <!---->
</template>

<script setup lang="ts">
// fully accessible
const { somePrivateKey } = useRuntimeConfig()
const { ssrContext } = useNuxtApp()
// you don't need `if (import.meta.server)` here
setResponseHeader(ssrContext.event, 'hello', 'VueAmsterdam !')
</script>
```

::

---

# Avoid shipping javascript chunks to your client !

<img src="/assets/islands-chunk.jpg" class="w-1/2 mx-auto" >


---
layout: with-title
title: Drawbacks
---
# Nuxt islands does have some drawbacks

- No client code 
- Your app instance is not linked to the island component

<img src="/assets/island-ssr-flow.png" class="rounded-xl w-3/4 mx-auto" >

---
layout:  with-title
title: "How does it work ?"
---

# Enable the feature

<div class="mt-30" />

::Window
```ts
export default defineNuxtConfig({
  experimental: {
    componentIsland: true
  }
})
```
::

---

# Two ways of using islands

- `<NuxtIsland>` component
- server components

---

# `NuxtIslands`

- Low level
- Components are within the `components/islands` directory
- Or with `island: true` when using `addComponent`

```md
|- components
--| islands
----| Counter.vue
```


<div class="grid grid-cols-2 gap-2">

::Window{filename="components/islands/Counter.vue"} 
```vue
<template>
  <div>
    {{ count }} x {{ multiplier }} = {{ count * multiplier }}
  </div>
</template>

<script setup lang="ts">
defineProps<{
  multipler: number
  count: number
}>()
</script>
```
::

::Window
```vue
<template>
  <NuxtIsland name="Counter" :props="{ multiplier: 5 }" />
</template>

<script setup lang="ts">
</script>
```
::

</div>

---

# Server components

- Higher level
- use `.server.vue` suffix in your component name
- used as a "normal" component

<div class="grid grid-cols-2 gap-2">


::Window{filename="components/Counter.server.vue"} 
```vue
<template>
  <div>
    {{ count }} x {{ multiplier }} = {{ count * multiplier }}
  </div>
</template>

<script setup lang="ts">
defineProps<{
  multipler: number
  count: number
}>()
</script>
```
::


::Window
```vue
<template>
  <NuxtIsland name="Counter" :props="{ multiplier: 5, count: 1 }" />
</template>

<script setup lang="ts">
</script>
```
::

</div>

---
layout: with-title
title: What really happens ?
---
## SSR/Client-side:
- `<NuxtIsland>` makes a fetch request to the Nuxt Server

<div class="mt-5" />

## Server side :
- Request will go through the nitro renderer event handler
- A Nuxt instance and Vue app will be created which only render the component
- The handler construct the response and send it back as JSON

<div class="mt-5" />

## Client side:
- Receive, read and cache the response
- Render the html as static Vnode

---
layout: with-title
title: "What does NuxtIsland provides ?"
---

# Full support for slots and scoped slots

::Badge{type="success"}
Nuxt `3.5`
::

<img src="/assets/island-slot.png" class="w-1/2 mx-auto mt-10" >

---

# Remote Island

::Badge{type="success"}
Nuxt `3.7`
::

<img src="/assets/remote-island.png" class="w-1/2 mx-auto mt-5" >

---

# Client components

::Badge{type="success"}
Nuxt `3.8`
::

<div class="mt-10" />

::window{filename="components/Content.server.vue"}

```vue
<template>
  <div>
    <UPageBody prose>
      <ContentRenderer :value="page" />
      <!-- Just use `nuxt-client` to load a component client side -->
      <Counter nuxt-client />
    </UPageBody>
  </div>
</template>

<script lang="ts" setup>
const props = defineProps<{
  path: any
}>()

const { data: page } = await useAsyncData(props.path, () => queryContent(props.path).findOne())
if (!page.value) {
  throw createError({ statusCode: 404, statusMessage: 'Page not found', fatal: true })
}
</script>
```

::

---

# Global client components

::Badge{type="success"}
Nuxt `3.11`
::
<div class="mt-10" />

<div class="grid grid-cols-2 gap-4">
<div>

::Window{filename="nuxt.config.ts"}
```ts
export default defineNuxtConfig({
  experimental: {
    componentIsland: {
      selectiveClient: 'deep'
    }
  }
})
```
::

</div>

<div>
<img src="/assets/globalcomponents.png" class="w-3/4" >


- `nuxt-client` becomes a reserved attribute
- Declare component as loadable client-side anywhere

</div>
</div>

---

# Island pages
::Badge{type="success"}
Nuxt `3.11`
::

<div class="mt-10">

::Window{filename="pages/index.server.vue"}
```vue
<template>
  <div>
    <UPageBody prose>
      <ContentRenderer :value="page" />
    </UPageBody>  
  </div>
</template>

<script setup lang="ts">
definePageMeta({
  island: true
})

const { data: page } = await useAsyncData(props.path, () => queryContent(props.path).findOne())
if (!page.value) {
  throw createError({ statusCode: 404, statusMessage: 'Page not found', fatal: true })
}
</script>
```
::


</div>



---

