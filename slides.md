---
theme: seriph
background: ""
class: "bg-gradient-to-r from-gray-100 to-gray-400 dark:from-gray-700 dark:to-gray-900 p-0"
highlighter: shiki
lineNumbers: false
drawings:
  persist: false
transition: slide-left
title: SvelteKit intro
---

# Web development, streamlined

## An introduction to SvelteKit

<img class="mt-20" src="/svelte-machine.png" />

---

# About me

- Svelte maintainer
- Senior Software Engineer at Ordergroove
- pianist
- cat lover

TODO pics

---

# What is Svelte?

- component-based JS framework
- uses a compiler

<!--
- [ show of hands — who has heard of Svelte? used Svelte? ]
- So Svelte has been getting fairly well known these days, but in case this is your first time hearing about it — it is a component-based JavaScript framework like React and Vue, but the major difference is instead of interpreting your component code with a runtime it ships to the browser, it compiles your components into vanilla JavaScript at build time. So on average, this makes for applications that are typically smaller and faster than applications built with the other big frameworks.
-->

---
layout: fact
---

# 3KB

(gzipped and compressed)

---

# Minimal boilerplate

```svelte {all|2,13|3,7|3,10-12|all}
<script>
  export let label = 'Increase count';
  let count = 0;
  $: doubled = count * 2;
</script>

<p>The count is {count}</p>
<p>Doubled: {doubled}</p>

<button on:click={() => {
  count = count + 1;
}}>
  {label}
</button>

<style>
  button {
    padding: 0.5rem;
  }
</style>
```

<!--
- And because it’s a compiler, the component authoring experience can also be optimized for simplicity and ease of use

TODO solidify which lines to highlight

In a .svelte file
Props, use in template
State
Updating state
Reactive state
Scoped styles

Svelte is my favorite way to write UI components, but when building a web app you often need more than just a way to write components. That’s where SvelteKit comes in
-->

---

# What SvelteKit handles

- router
- data loading
- build optimizations
- form handling
- SSR
- code splitting
- deployment
- and more!

TODO some sort of image - legos?

<!--
SvelteKit handles the layer on top of your Svelte components 

Svelte just says here’s a component language, it’s up to you to wire everything together, figure out how to deploy it. SvelteKit provides structure and takes care of the boring bits, and it’s the Svelte team’s recommended way to build any app with Svelte.

Svelte is individual legos, SvelteKit is the foundation for a castle (Lego Knights Kingdom set) or an instruction manual.
-->

---
class: bg-white
---

<div class="wrapper">

<img src="/nuxt-logo.png">
<img src="/nextjs-logo.png">
<img src="/remix-logo.png">

</div>

<style>
  .wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2rem;
  }
  img {
    flex-shrink: 0;
    max-width: 500px;
  }
</style>


<!--
If you’re familiar with the React ecosystem, think of it like NextJS or Remix, except unlike those frameworks Svelte and SvelteKit are made by the same team.
-->

---

# Plan for today

- Understand what SvelteKit brings to the table
- Brief demo

<img src="/learn-svelte-dev.png" class="pt-10">

<!--
Will be doing a live demo to see it in action, but this isn’t the right place for a full tutorial. If you want that, learn.svelte.dev
-->

---
layout: fact
---

# Values > Syntax

<!--
One way of doing this would to just show all of SvelteKit's syntax. Here's what a data loader looks like, here's what a route file looks like. And we'll be doing that, but I want to go deeper

Syntax matters — I like Svelte because of its concise syntax. But it’s more interesting to understand why than what.

Lets understand what SvelteKit prioritizes

TODO elaborate
-->

---
layout: fact
---

# You shouldn't have to configure your build

... or your **dev server**, or your **deployment**

<!--
Build configuration can be one of the most frustrating parts of web dev for me. Feels like magic -- just need to figure out the right incantation
Thankfully we've reached a point where I don't need to care a lot about that, at least in my hobby work
-->

---
class: text-4xl
layout: center
---

- optimized build
- code splitting
- extremely fast dev server with HMR

<br>
... with no config required on your part

<!--
And SvelteKit can't take the credit here
-->

---
layout: center
---

<img src="/vite.png">

<!--
All of this is thanks to Vite, front-end tooling that is being built on by tons of tools across the ecosystem

Astro, Nuxt, Solid

As well as this slide framework!
-->

---
layout: center
---

<img src="/sveltekit-wizard.png">

<!--
Beyond build tooling, when you create a new SvelteKit app you can setup TypeScript, testing tools, Prettier, and ESLint
-->

---
layout: center
---

<img src="/deploy-anywhere.png">

<!--
Similarly, deployment shouldn't be a hassle. SvelteKit has the concept of deployment "adapters" to support simple deployments to any supported platform
-->

---

```js
import adapter from 'svelte-adapter-foo';

const config = {
    kit: {
        adapter: adapter()
    }
};

export default config;
```

<br>

```diff
---import adapter from 'svelte-adapter-foo';
+++import adapter from 'svelte-adapter-better';

const config = {
    kit: {
        adapter: adapter()
    }
};

export default config;
```

<!--
Here's what using an adapter looks like

Swapping with a single line change
-->

---
layout: fact
---

# Strong conventions
(one way to do things)

<!--
minimize API surface area — less to learn and choose between
-->

---

# Directory-based routing

```text {all|2-5|3|4-5|all}
src/
├─ routes/
│  ├─ +page.svelte
│  ├─ about/
│  │  ├─ +page.svelte
```

<br>

```html
<a href="/">Home</a>
<a href="/about">About</a>
```

<!--
Folders create routes
<a> link between them - no link component
-->

---

# Loading data: the load function

```text {all|5}
src/
├─ routes/
│  ├─ about/
│  │  ├─ +page.svelte
│  │  ├─ +page.server.js
```

<br>

<div class="grid grid-cols-2 gap-6">

<div>
+page.server.js

```js
export async function load() {
	const items = await api.getItems();
	return {
		items
	};
}
```
</div>

<div>
+page.svelte

```svelte
<script>
  export let data;
</script>

<ul>
{#each data.items as item}
  <li>{item}</li>
{/each}
</ul>
```
</div>

</div>

---

# Because this is a convention, SvelteKit can improve DX and UX

SvelteKit understands what data is needed for any given page

- typesafe data loading
- preloading data

<br>

<img src="/typesafety.png">

---

TODO:
- forms?
- "SK doesn't want to have a convention for everything"?

---
layout: fact
---

# The client/server boundary matters

---

```js {all|1-8|10-30}
export async function loader({ request }) {
  return getProjects();
}

export async function action({ request }) {
  const form = await request.formData();
  return createProject({ title: form.get("title") });
}

export default function Projects() {
  const projects = useLoaderData();
  const { state } = useNavigation();
  const busy = state === "submitting";

  return (
    <div>
      {projects.map((project) => (
        <Link to={project.slug}>{project.title}</Link>
      ))}

      <Form method="post">
        <input name="title" />
        <button type="submit" disabled={busy}>
          {busy ? "Creating..." : "Create New Project"}
        </button>
      </Form>
    </div>
  );
}
```

<!--
Some frameworks let you write server-only and client code in the same file
e.g. Remix
bundling magic splits out the server code from the client code

and this is great and the experimentation is exciting, but SK intentionally does not allow that
TODO elaborate

- separate files, separate contexts
- mental model gets fuzzy
- security implications
-->

---
layout: fact
---

## Any code you write inside a `.server` file will stay on the server

If you try to import code from a `.server` file into code that gets sent to the client, you will get an error.

<!--
Separate files, separate contexts
-->

---
layout: center
---


```js
import { API_KEY } from '$env/static/private';
```


<style>
  pre {
    --slidev-code-font-size: 1.5rem;
    --slidev-code-line-height: 1.5;
  }
</style>

<!--
Built in environment variable handling that will also warn you if it gets included where it shouldn't
-->

---
layout: fact
---

# Make it easy to work with the grain of the web


---

# Using web standard objects

- Request & Response
- URL
- FormData

<!--
The way you interact with these objects in regular JS is the same as in SvelteKit
Wasn't always like this - used to have custom URL object for example
transportability of knowledge
-->

---
layout: fact
---

# `<a>` and `<form>`

<style>
  h1 {
    line-height: 1.5 !important;
  }
</style>

<!--
SK uses a to link between things, form for submitting data
Nothing is stopping you from using other ways if you want

But by using web primitives we make for a more resilient app
-->

---
layout: image
image: /everyone-has-js.png
---

https://www.kryogenix.org/code/browser/everyonehasjs.html

<style>
  .slidev-layout {
    /* https://github.com/slidevjs/slidev/issues/798 */
    background-size: contain !important;
  }

  a {
    position: absolute;
    bottom: 0.5rem;
    @apply bg-white dark:bg-black;
  }
</style>

<!--
Everyone has JS, right? No
If all your logic is in JS, if your JS fails to load, then you're out of luck
But if your app is SvelteKit, the defaults will ensure some functionality (SSR, links to navigate, forms submit data)
-->

---
layout: fact
---

# Defaults matter...

make the right thing easy

<!--
Most devs don't touch the defaults
Most devs won't read all your documentation
It's important that you can get a good result without all that - put the site in a strong place to begin with

- Encouraging the use of links and forms matter
    - The average dev won’t do everything that goes into `use:enhance` if they had to set it up themselves
    - And that’s not to shame them — the average dev needs to get shit done!
-->

---

# What are those defaults?

- links and (enhanced) forms
- real URLs
- SSR
- preloading data
- client side routing (but more accessible)

<!--
Mostly stuff we talked about

Client-side routing in particular - many frameworks that default to client-side routing don't make it accessible
- no moving focus when changing page
- no announcing new routes

we try to (though I'd like to see us do better)
-->

---
layout: fact
---

# ... but so does flexibility

the web is not just one thing

---
layout: fact
---

# Why choose?

---
layout: center
---

# Fully static or fully rendered on request

<img class="m-auto" src="/porque-no.jpg">

---

# Page options

<br>

```js
export const ssr = true; // server side rendering
export const csr = true; // client side rendering
export const prerender = false;
```

<style>
  pre {
    --slidev-code-font-size: 1.5rem;
    --slidev-code-line-height: 1.5;
  }
</style>

<!--
Can configure on a per page (or per directory of pages) basis

- landing page prerendered
- turn off ssr for admin portal
-->

---
layout: fact
---

# Putting the "Kit" in SvelteKit

<!--
Use the parts of SvelteKit that make sense for you
As much as I've talked about links and forms - If you want to build an SPA, use a different lib for data fetching and only use SvelteKit for the routing then that works too
-->

---

# Recap

- Build configuration made effortless
- Strong conventions
- Understand the client/server boundary
- Work with the grain of the web
- Defaults that set you up for success
- with the freedom to reconfigure those defaults as needed

---
layout: fact
---

# Demo time

---

# Why use SvelteKit?

- you want to build websites with Svelte
- or those principles sounded compelling to you