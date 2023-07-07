
---

```js {all|1|all}
import adapter from 'svelte-adapter-foo';

const config = {
    kit: {
        adapter: adapter()
    }
};

export default config;
```

<br>

<div v-click>

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

</div>

<!--
Here's what using an adapter looks like

Swapping with a single line change

So that's the configuration story, let's move on to what else SvelteKit values
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