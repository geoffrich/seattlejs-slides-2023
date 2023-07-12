
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

issues with this approach (continue slides through bullets)

this still works in SvelteKit but there's a better way
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

we want to be very clear about what is server code and what is client code

- clearer mental model
- separate files, separate contexts
- you don't have to understand rules around what is server and what is client 

maybe this will become more common, but for now this is what we think makes sense
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
