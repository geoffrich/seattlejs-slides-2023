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

<br>

<div class="images">

<img src="/cats.jpg" height="300" width="200">

<img src="/cats2.jpg" height="200" width="300">

</div>

<style>
  .images {
    display: flex;
    align-items: center;
    gap: 2rem;
  }
</style>

---

# What is Svelte?

- component-based JS framework
- uses a compiler
- smaller & faster* apps

<style>
  ul {
    font-size: 1.5rem;
  }
</style>

<!--
- [ show of hands — who has heard of Svelte? used Svelte? ]
- So Svelte has been getting fairly well known these days, but in case this is your first time hearing about it — it is a component-based JavaScript framework like React and Vue, but the major difference is instead of interpreting your component code with a runtime it ships to the browser, it compiles your components into vanilla JavaScript at build time. So on average, this makes for applications that are typically smaller and faster than applications built with the other big frameworks.
-->

---
layout: fact
---

# 3KB

(gzipped and compressed)

<!--
for instance, a Svelte "hello world" is under 3KB

Faster does have an asterisk - in the years since Svelte has come out, the gap has narrowed and now a framework like Vue is slightly ahead of Svelte when you look at the benchmarks
-->

---

# Minimal boilerplate

```svelte {all|2,6|2,6,9-11|2,3,6,7|9-19|all}
<script>
  let count = 0;
  $: doubled = count * 2;
</script>

<p>The count is {count}</p>
<p>Doubled: {doubled}</p>

<button on:click={() => {
  count = count + 1;
}}>
  Increment
</button>

<style>
  button {
    padding: 0.5rem;
  }
</style>
```

<!--
But for me, the reason I love svelte is not because it's the smallest or the fastest framework -- it does well there, but it's not #1

It's how productive it feels to write Svelte components.

Because it’s a compiler, the component authoring experience can also be optimized for simplicity and ease of use

This is what a Svelte component looks like

- In a .svelte file
- State
- Updating state
- Reactive state
- Scoped styles

That's Svelte, if it's new to you I recommend giving it a try

Svelte is my favorite way to write UI components, but when building a web app you often need more than just a way to write components. That’s where SvelteKit comes in
-->

---

# What SvelteKit handles

- router
- data loading
- build optimization
- form handling
- SSR
- deployment
- and more!

TODO some sort of image - legos?

<!--
SvelteKit - everything you need to build a full app or website

handles the layer on top of your Svelte components 

Svelte just says here’s a component language, it’s up to you to wire everything together, figure out how to deploy it. SvelteKit provides structure and takes care of the boring bits, and it’s the Svelte team’s recommended way to build any app with Svelte.

So you don't have to provide answers for all these things yourself

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
One way of doing this would to just show all of SvelteKit's syntax. Here's what a data loader looks like, here's what a route file looks like. And we'll be doing that, but I want to go beyond regurgitating syntax

Syntax matters — I like Svelte because of its concise-yet-readable syntax. But it’s more interesting to understand why than what.

Choosing a framework is more than just syntax

Lets understand the principles that make SvelteKit what it is

-->

---
layout: fact
---

# You shouldn't have to configure your build

... or your **dev server**, or your **deployment**

<!--
Build configuration can be one of the most frustrating parts of web dev for me. Feels like magic -- just need to figure out the right incantation, lots of trial and error

Thankfully we've reached a point where I don't need to care a lot about that, at least in my hobby work

By using SvelteKit, you automatically get...
-->

---
class: text-4xl
layout: center
---

- optimized build (tree shaking, minification, module preloading)
- code splitting (JS and CSS)
- extremely fast dev server with HMR

<br>
... with no config required on your part

<!--
- tree shaking - remove unused code from bundle
- module preloading - no import waterfalls

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

Vite is providing a baseline level of functionality so other teams in the ecosystem can innovate on what truly matters instead of reinventing CSS code splitting or whatever
-->

---
layout: center
---

<img src="/sveltekit-wizard.png">

<style>
  img {
    max-width: 700px;
  }
</style>

<!--
Beyond build tooling, when you create a new SvelteKit app you can setup TypeScript, testing tools, Prettier, and ESLint
-->

---
layout: center
---


<img src="/deploy-anywhere.png" >

<!--
Similarly, deployment shouldn't be a hassle. SvelteKit has the concept of deployment "adapters" to support simple deployments to any supported platform

Vercel, Netlify, Cloudflare, Azure, or as plain Node JS or a collection of static files

Changing deployment platforms can be a one-line change
-->

---
layout: fact
---

# Strong conventions
what do most apps need?

<!--
strong conventions around what's needed by all apps

just like Svelte is batteries-included for common component concerns like styling, SvelteKit is that for apps

most apps need a way to navigate between different pages, load data, mutate data

SK provides an answer for all of these things

by providing an answer:

- set devs up for success
- easier onboarding to projects using SvelteKit
- batteries included
-->

---

# Directory-based routing

folders create routes

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

To know what renders at any given URL, you go to the corresponding folder

`<a>` link between them - no link component

by default, SvelteKit will server render each route for the initial request, for good SEO and so that users see content right away

and then after the initial load, SK will use client-side navigation for a snappy, app-like experience
-->

---

# Loading data: before SvelteKit

```svelte
<script>
  import { onMount } from 'svelte';

  let data;

  onMount(() => {
    fetch('/api/items')
      .then(r => r.json())
      .then(result => {
        data = result;
      });
  });
</script>
```

<br>

<v-clicks>

- doesn't start until JS parsed & component rendered
- boilerplate
- users without JS are out of luck

</v-clicks>

<!--
most apps need to load data - here's how you'd do that in pure svelte

parsing/loading/error handling all by yourself

issues with this approach

this still works in SvelteKit but there's a better way
-->

---

# Loading data: the load function

```text {all|3-4|3,5}
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

<!--
loads the data for the page

when you navigate to this route, SK will call the load function

available in the data prop
-->

---

# Because this is a convention, SvelteKit can improve DX and UX

SvelteKit understands what data is needed for any given page

- preloading data (before rendering even happens)
- server-side rendering
- typesafe data loading

<br>

<img src="/typesafety.png" v-click>

---

# Mutating data: actions

<div class="grid grid-cols-2 gap-6">

<div>
+page.svelte

```svelte {1-5|6-23}
<form method="POST" action="/?login">
  <label>Username <input type="text" name="username"></label>
  <label>Password <input type="password" name="password"></label>
  <button>Log in</button>
</form>

<script>
  import { enhance } from '$app/forms';
</script>

<form method="POST" action="/?login" use:enhance>
  <label>Username <input type="text" name="username"></label>
  <label>Password <input type="password" name="password"></label>
  <button>Log in</button>
</form>
```
</div>

<div>
+page.server.js

```js
export const actions = {
  login: async ({ request }) => {
    // log the user in
    const data = await request.formData();
    const username = data.get('username');
    const password = data.get('password');
    await performLogin({ username, password });
  }
}
```

<br>

<div v-click>

- with `use:enhance`, the form will submit without reloading the page
- can pass a callback to customize the behavior

</div>

</div>

</div>

<!--
just like most apps need to load data, most apps need to mutate data

form has seen a bit of a comeback lately in the JS framework world (Remix, Next, Solid Start)

SK also likes forms

- progressive enhancement
-->

---
layout: fact
---

# The client/server boundary matters

---

(this is Remix, not SvelteKit)
```js {all|1-8|10-30} {maxHeight:'400px'}
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
we saw +page.server.js before for load functions - the .server indicates that you're in a server-only context

Separate files, separate contexts
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
    @apply bg-black;
  }
</style>

<!--
Everyone has JS, right? No

very few people disable JS. but it's common for people to be in situations where JS is slow to load or even fails to load

If all your logic is in JS, if your JS fails to load, then you're out of luck

But if your app is SvelteKit (or another framework that prioritizes PE), the defaults will ensure some functionality (SSR, links to navigate, forms submit data)
-->

---
layout: fact
---

# Defaults matter...

make the right thing easy

<!--
- Most devs don't touch the defaults
- Most devs won't read all your documentation
- It's important that you can get a good result without all that - put the site in a strong place to begin with

- Encouraging the use of links and forms matter
    - The average dev won’t do everything that goes into `use:enhance` if they had to set it up themselves
    - And that’s not to shame them —  but by making this the conventional, default way we set them up for success
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

Defaults <==> conventions - by having an answer for "how do I load data / how to I mutate data" that encourages best practices, we can increase the performance of the average SK app

Client-side routing in particular - many frameworks that default to client-side routing don't make it accessible
- no moving focus when changing page
- no announcing new routes

we try to (though I'd like to see us do better)
-->

---
layout: fact
---

# ... but so does flexibility

the web is not just one thing, so why choose?


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
We think SSR makes sense for a lot of apps. but not for everything

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
- Understand the client/server boundary
- Strong conventions
- Work with the grain of the web
- Defaults that set you up for success
- The freedom to reconfigure those defaults as needed

---
layout: fact
---

# Demo time

<!--
- artist and album routes
- returning data, available in page
- form action
- use:enhance
- customizing use:enhance for optimistic UI
- and it works without JS (which is not just a party trick)
-->

---

# Where to next?

- the docs: svelte.dev / kit.svelte.dev
- the tutorial: learn.svelte.dev
- Svelte discord: svelte.dev/chat

## my stuff

<br>

- site: geoffrich.net
- twitter: @geoffrich_
- mastodon: @geoffrich@front-end.social

---
layout: fact
---

# Thanks!
