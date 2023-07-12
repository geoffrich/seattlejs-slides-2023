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

a _component-based JS framework_ that uses a <span class="svelte">compiler</span>

<style>
  h1 {
    text-align: center;
    font-size: 3rem !important;
  }

  p {
    text-align: center;
    display: block;
    margin-top: 7rem !important;
    font-size: 3rem;
    line-height: 1.5 !important;
    opacity: 1 !important;
  }

  .svelte {
    background-color: hsl(15, 100%, 40%);
    color: white;
    padding: 0.2rem 0.6rem;
    font-weight: bold;
  }
</style>

<!--
- [ show of hands — who has heard of Svelte? used Svelte? ]
- So Svelte has been getting fairly well known these days, but in case this is your first time hearing about it — it is a component-based JavaScript framework like React and Vue, but the major difference is instead of interpreting your component code with a runtime it ships to the browser, it compiles your components into vanilla JavaScript at build time. So the advantage of this is that you can ship less JavaScript to your users, and your application has to do less work because it has compiled away a lot at build time
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
[ don't dwell too long on this ]

But for me, the reason I love svelte is not because it's the smallest or the fastest framework -- it does well there, but it's not #1

It's how productive it feels to write Svelte components.

Because it’s a compiler, the component authoring experience can also be optimized for simplicity and ease of use

This is what a Svelte component looks like

- In a .svelte file
- State
- Updating state
- Reactive state
- Scoped styles (batteries included)

That's Svelte, if it's new to you I recommend giving it a try

Svelte is my favorite way to write UI components, but when building a web app you often need more than just a way to write components. 
-->

---

# Production app requirements

<v-clicks>

- router
- data loading
- build optimization
- form handling
- SSR
- deployment
- and more!

</v-clicks>

<style>
  ul {
    font-size: 1.5rem;
  }

</style>

<!--
There are all these things that go into building a full web app that a component framework doesn't handle

while you can answer all these yourself or find packages on npm, it would be nice to have a framework that already answers these questions so you don't have to

and that's what SvelteKit does
-->

---
layout: center
---

<img src="/sveltekit-logo.png">

<!--

SvelteKit brings everything you need to build a full app or website

Svelte just says here’s a component language, it’s up to you to wire everything together, figure out how to deploy it. SvelteKit provides structure & conventions and lets you spend your time building instead of configuring and choosing between packages on npm

it’s the Svelte team’s recommended way to build any app with Svelte.

-->

---
class: bg-white
---

<div class="wrapper">

<img src="/nextjs-logo.png">
<img src="/remix-logo.png">
<img src="/nuxt-logo-big.png">

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
    max-width: 450px;
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

It's also values -- express themselves in code & what you ship

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
- extremely fast dev server that quickly updates with changes

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
Beyond build tooling, when you create a new SvelteKit app you can automatically configure TypeScript, testing tools, Prettier, and ESLint
-->

---
layout: center
---


<img src="/deploy-anywhere.png" >

<!--
Similarly, deployment shouldn't be a hassle. SvelteKit has the concept of deployment "adapters" to support simple deployments to any supported platform

Vercel, Netlify, Cloudflare, Azure, or as plain Node JS or a collection of static files -- and more from the community

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

```js {all|2-5}
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

```svelte {all|2|2,6-8}
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
similarly, most apps need a way to load data

in SK: the load function

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

<style>
  ul {
    font-size: 1.5rem;
  }
</style>

---

# Mutating data: actions

<div class="grid grid-cols-2 gap-6">

<div>
+page.svelte

```svelte {1-7|8-13|8-27}
<form method="POST" action="/?login">
  <label>Username 
    <input type="text" name="username"></label>
  <label>Password 
    <input type="password" name="password"></label>
  <button>Log in</button>
</form>

<script>
  import { enhance } from '$app/forms';
</script>

<form method="POST" action="/?login" use:enhance>
  <label>Username 
    <input type="text" name="username"></label>
  <label>Password 
    <input type="password" name="password"></label>
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

</div>

</div>

<!--
just like most apps need to load data from an API, most apps need to submit updates to that data

and that's where forms come in

form has seen a bit of a comeback lately in the JS framework world (Remix, Next, Solid Start)

SK also likes forms

while you can submit data with a regular fetch call if you want to

forms provide better defaults - they still function even if your JS fails

to submit data in SK app: create a form, declare a form action in +page.server.js to handle that form submission

when you submit the form, your action can read the submitted data and handle it

call out significance of .server.js -- so you know you're in a server only context, free to access DB directly or use sensitive keys, whatever

but regular forms aren't necessarily the best user experience

which is why SK provides built in progressive enhancement

so use:enhance - when JS available, submit the form using a fetch call instead

best of both worlds -- it's resilient and will work when JS fails, but will enhance to a better user experience when it can

ok, that was a lot, check out the tutorial. happy to answer any questions later.
-->

---
layout: fact
---

# Make it easy to work with the grain of the web

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
I've talked a lot about JS not being available

And that's not just users who have disabled JS, but also all the cases where JS fails

If all your logic is in JS, if your JS fails to load, then you're out of luck

But if your app is SvelteKit (or another framework that prioritizes PE), the defaults will ensure some functionality (SSR, links to navigate, forms submit data)
-->

---

# Using web standard objects

- Request & Response
- URL
- FormData

<style>
  ul {
    font-size: 1.5rem;
  }
</style>

<!--
beyond links and forms, much of Svelte's API is the browser standard objects

no proprietary request/response/url

The way you interact with these objects in regular JS is the same as in SvelteKit

Wasn't always like this - used to have custom URL object for example

transportability of knowledge
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

<style>
  ul {
    font-size: 1.5rem;
  }
</style>

<!--
Mostly stuff we talked about

Defaults <==> conventions - by having an answer for "how do I load data / how to I mutate data" that encourages best practices, we can increase the performance of the average SK app
-->

---
layout: fact
---

# ... but so does flexibility

the web is not just one thing, so why choose?

---
layout: fact
---

# Defaults, not demands

putting the "Kit" in SvelteKit

<!--
we do have these defaults and conventions, but we recognize they don't make sense for every app

Use the parts of SvelteKit that make sense for you

As much as I've talked about links and forms - If you want to build an SPA, use a different lib for data fetching and only use SvelteKit for the routing then that works too

SvelteKit is the framework that grows with you! Start simple and use more features as you need them.

this also extends to how your app is served -- you don't need a server

-->

---
layout: center
---

# Fully static or fully rendered on request

<img class="m-auto" src="/porque-no.jpg" v-click>

<!--
you can build static sites / SPAs with SK too

but it's not just that you can choose this at the app level: static site or server site

you can configure this on a per page basis
-->

---

# Page options

<br>

+page.js

```js {1|all}
export const prerender = true;
export const ssr = true; // server side rendering
```

<style>
  pre {
    --slidev-code-font-size: 1.5rem;
    --slidev-code-line-height: 1.5;
  }
</style>

<!--
prerender: control whether page is turned into HTML at build time

similarly: SSR

We think SSR makes sense for a lot of apps. but not for everything

Can configure on a per page (or per directory of pages) basis

- landing page prerendered
- turn off ssr for admin portal
-->

---

# Recap

- Build configuration made effortless
- Strong conventions
- Work with the grain of the web
- Defaults that set you up for success
- The freedom to reconfigure those defaults as needed

<style>
  ul {
    font-size: 1.5rem;
  }
</style>

---
layout: fact
---

# Demo time

<!--
- artist and album routes
- data preloading
- returning data, available in page
- form action
- use:enhance
- customizing use:enhance for optimistic UI (gloss over)
-->

---

# Where to next?

- the tutorial: learn.svelte.dev
- the docs: svelte.dev / kit.svelte.dev
- Svelte discord: svelte.dev/chat

## stuff we didn't cover
- layouts (and loading data in them)
- advanced routing
- customizing use:enhance
- data streaming
- client-only loads
- API routes
- middleware
- environment variables
- and more!

---

# my stuff

- site: geoffrich.net
- twitter: @geoffrich_
- mastodon: @geoffrich@front-end.social

## slides / demo: geoffrich.net/posts/seattlejs-2023

---
layout: fact
---

# Thanks!
