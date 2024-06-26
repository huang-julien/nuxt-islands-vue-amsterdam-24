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
 

<!--

Hello !
So happy to be here today, it's actuelly my first time in Amsterdam and in such a a big conference. So glad to meet you all. 
Many of you probably don't know who I am so, I should start to introduce myself.

-->

---
layout: text-image
content-wrapper-class: w-3/4
img-class: "!rounded-full border-4 border-solid border-gold"
media: /assets/profile.jpg
---

# Hey 👋 I'm Julien Huang
 
- ### Frontend developer at <LeetchiLogo class="h-6 text-[#f7c0b9] mb-1 inline" />
- ### Open-source enthusiast
- ### <ri-team-fill /> Nuxt Core team member <logos-nuxt-icon />

<div class="mt-15" />

Other hobbies
- Playing to A LOT of video games <emojione-v1-keyboard-and-mouse />
- Practicing flute and piano <material-symbols-music-note/> 
- working out <guidance-weightlifting/>


<!--

My name is Julien. I’m currently working as a frontend developer at Leetchi in France and I’m also a nuxt core team member since last month and i was a nuxt insider since a year.

Just a bit about myself, I started to learn web developement after the covid lockdown in France, so i’m a developer since… like 3 year and a half; Soon 4. It's probably the best decision i've ever made

In addition to my job as a Frontend developer, I also enjoy contributing to open-source projects (mainly nuxt), and I have been doing so for nearly two years. Aside from my interest in open-source, I also enjoy practicing the piano and flute, as well as working out and I also love playing video games.

So within the Nuxt Core repository, I’ve been working a lot on Nuxt island since over a year and i’d like to share with you what nuxt island is, why does it exist and  how does it works, maybe if we have enough time, i can probably show you a small demo.

-->

---
layout: text-image
media: /assets/frameworks-everywhere.jpg
imgWrapperClass: w-1/2
---

::title::

# Rise of frontend frameworks

::default::

<v-click hide>

::TitleOverlay

# A story about server components

::

</v-click>

- Untied frontend from backend
- Frontend become much more flexible
- Great level of interactivity

<div class="mt-5" />

- Everything was pushed client-side

<!--
let’s start with a story of server only components

Today, most of you may have heard a lot about islands components and server components in the web developement. In facts, it is becoming more and more common today for web developers. Especially for nextJS developer since it is now default.

So... with the rise of SPA, we uncoupled comletly the frontend and backend, it made frontend much more flexible, brought a great level of interactivity for users and also a better user experience. 

Even things that is supposed to be served by the server directly to the app such data from a databse
-->

---
layout: text-image
media: /assets/stronks-metaframeworks.jpg
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

<!--
and lastly theses last years we had the rising (not of the shield hero) but of meta-frameworks which comes to recouple frontend and backend for the initial request. most of them like nuxt aims to bring a way to easily handle server side rendering for developers and bring a whole new level of developer experience compared to the lower level of JS frameworks

The only isssue is that the complexity of your application will increase even further because you have know 2 context, one server and one client.

Now If we think about nuxt, we have a server that renders application and components server side. 
When you mount it client-side, we must import all javascript that is needed to render the first state of your app. Even if it does not have any interactivity at all and sometimes, this can be quite annoying. After all no interactivity i wouldn't want to load the whole javascript chunk of a component

This is explained by the process of hydration

-->

---
layout: with-title
title: Hydration
---

# What is it ?

Hydration is the process by which frameworks initialize an application on top of server-rendered HTML.

<img src="/assets/alex.png" class="absolute w-1/2 rotate-320 left-130" />

<img src="/assets/finally.jpg" class="w-1/2 mx-auto rounded-xl" />

<!--

As explained by Alex this morning, 

 

Hydration is the process by which frameworks initialize an application on top of html that is already rendered.
Most server-side rendered (SSR) app require hydrating the received HTML before mounting the app client-sid  to have the same state of render as the SSR app and so to attach every listeners to the DOM element.
-->

---

# How does it work ?

<HydrationFlow  class="my-10" />

## At Hydration step

- Mount each components
- When mounting, Vue will perform a comarison between the vnode and the DOM element

<!--

When your browser request a page to your server, an application will be initialized server side to generate your HTML. Nuxt will then generate and send the HTML. Then your browser receive it and will load the javascript files linked within it.

So hydration means in reality initializing your application twice. 
- once server-side
- once client-side

When Vue mount on your rendered HTML. At component rendering step, it will perform a comparison between the VNodes that your components render function has returned and the current DOM.

if there’s a mismatch, vue will try to rerender the mismatched part once again or sometime the whole app but this can leads to bugs we should avoid it for performance reason because interactivity for your users will be delayed, there will be layout shift etc...

So sometimes we create components that are very heaving in terms of bundle for rendering but not interactive nor dynamic at all, in any context of their usages, and this is especially true when using things like CMS which often only renders static content. 

-->

---

# Here comes server only components

- rendered only server-side
- sent in a format that will be read by the framework or a by a custom component
- render the result as static HTML
- non-interactive by default

<!--

So server only components are here to save your day. 
The idea is to have components that is rendered server side and then sent to the browser any formformat. Then either the framework or a component will handle the rendering of the result component without loading it’s javascript.

-->
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

<!--
In the world of react, they release RSC since 2020. They are using an ast streamed by the server to describe the Virtual node tree.

We do have something quite equivalent in Nuxt called Nuxt island which uses JSON response to render static html.

For those who tried Astro, Nuxt Island is basically the reverse thing. 

Astro islands are small portions of interactive components within static html, Nuxt Islands are portions of static html within an interactive single page application

-->

---
layout: with-title
title: Benefits
---

# Safely write server code within your component 

- only run server-side
- safe access to private configuration without risking leaks

::window{filename="components/island/YourIsland.vue"}

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

<!--
So what are the benefits of using it ?

First, you can safely write server only code within your component, since it it run only server-side. 
On nuxt it means that you have access to anything that is supposed to be server-side including thing such as a database access or  all your private runtime config;
 Of course this means that you won’t have any access to anything that is related to a client environement, you can't do any client side actions and any client side hooks such as `onMounted`

-->

---

# Avoid shipping javascript chunks to your client !

<img src="/assets/islands-chunk.jpg" class="w-1/2 mx-auto" >

<!--

And the main benefits is to avoid shipping  chunks of javascript to your browser.

Because everything it only rendered server side and we don't make it interactive, no javascript chunk will be imported. 

So the load time of your app will be reduced. And even the time for your app to be fully interactive can be reduced since at hydration step, vue will simply perform a quick comparison without 
attaching any listeners

-->


---
layout: with-title
title: Specificities of Nuxt islands
---

# Specificities of Nuxt islands

- At the moment, some islands features such as slots support are only available with SFC
- Your app instance is not linked to the island component

<img src="/assets/island-ssr-flow.png" class="rounded-xl w-3/4 mx-auto" >

<!--

NuxtIsland does have some other specifities...

First, some nuxt-island features such as slots or client components which will be explained later are only available with SFC because it need some file transformation that is only applied to SFC.

and second, an island component is completly isolated from your "main" nuxt app instance. It means that your island component is not able to have any impact such as modifying injected variables, useState data or accessing to your main app plugin.

And i'll show you a bit later why

-->

---
layout:  with-title
title: "How to use Nuxt islands ?"
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

<!--

Let's see how to use nuxt island

First  you have to enable the feature within your nuxt configuration.

To enable it you have to set `experimental.componentIsland` to true.
-->

---

# Two ways of using islands

- `<NuxtIsland>` component
- server components

<!--

There actually two ways of using island

first with the <nuxtIsland> component 
and then with server components

-->

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

<v-click>

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

</v-click>

<!--

Let's starts with the nuxt island component.

So the NuxtIsland component is a Low level way of using island components.

Everything within the components/island directory will be registered as island. Or if you are a module author or if you just want to use nuxt hook or the `addComponent` from nuxt/kit, just set the island field to true when declaring your component.


-->

---

# Server components

- Higher level
- use `.server.vue` suffix in your component name or set `mode` to `server`
- used as a "normal" component

<v-click>

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
  <!-- this is server only !-->
  <Counter :count="3" :multiplier="5" />
</template>

<script setup lang="ts">
</script>
```
::

</div>

</v-click>

<!--

And then we have Server components.

These are a higher level of island components, in reality it's a simple wrapper around NuxtIsland.

When you have a server component, to call it, you simply write it like any "normal" component 

The main advantage of server components is that you'll keep all type inference from typescript such as props or slot and event data passed from scoped slots !

So this is something not available on nuxt islands, the name field for exemple is not typed...
wait i'm pretty sure there's a way to do it, so i'll say "yet"
-->

---
layout: with-title
title: What really happens ?
---

Nuxt exposes an endpoint which starts by `/__nuxt_island`

<v-click>

## In you "main" nuxt app:
- `<NuxtIsland>` makes a fetch request to the Nuxt Server

<div class="mt-5" />

</v-click>
<v-click>

## Server side :
- Request will go through the nitro renderer event handler
- A Nuxt instance and Vue app will be created which only render the component
- The handler construct the response and send it back as JSON

</v-click>
<div class="mt-5" />
<v-click>

## In you "main" nuxt app:
- `<NuxtIsland>` Receive, read and cache the response
- Render the html as static Vnode

</v-click>

---
layout: with-title
title: "What does features NuxtIsland provides ?"
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

<TwoCols class="gap-5">

<img src="/assets/remote-island.png" class="mx-auto mt-5" >

<div>

<v-click>

::Window{filename="nuxt.config.ts"}
```ts
export default defineNuxtConfig({
  experimental: {
    componentIslands: {
      remote: true
    }
  }
})
```
::

</v-click>

<v-click>

::Window
```ts
interface NuxtIslandResponse {
  id?: string
  html: string
  state: Record<string, any>
  head: {
    link: (Record<string, string>)[]
    style: ({ innerHTML: string, key: string })[]
  }
  props?: Record<string, Record<string, any>>
  components?: Record<string, NuxtIslandClientResponse>
  slots?: Record<string, NuxtIslandSlotResponse>
}
```
::

</v-click>


</div>

</TwoCols>


---

# Client components

::Badge{type="success"}
Nuxt `3.8`
::

<div class="mt-10" />

<div class="grid grid-cols-2 gap-5">

::Window{filename="nuxt.config.ts"}
```ts
export default defineNuxtConfig({
  experimental: {
    componentIsland: {
      selectiveClient: true
    }
  }
})
```
::

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
</div>

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
const { data: page } = await useAsyncData(props.path, () => queryContent(props.path).findOne())
if (!page.value) {
  throw createError({ statusCode: 404, statusMessage: 'Page not found', fatal: true })
}
</script>
```
::


</div>


---
layout: with-title
title: "Some advices"
---

<v-clicks>

<p> Islands are not default and are not planned to be default</p>
<p>Don't use islands everywhere and for everything</p>
<p> Sometimes, the payload is even heavier than sending your bundle
</p>

</v-clicks>

---
layout: center
---

# Thank you ! ❤️

<mdi-github /> huang-julien <br>

<icon-park-twitter /> JulienHuang_dev
