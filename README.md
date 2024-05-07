# Welcome to [Slidev](https://github.com/slidevjs/slidev)!

To start the slide show:

- `npm install`
- `npm run dev`
- visit http://localhost:3030

Edit the [slides.md](./slides.md) to see the changes.

Learn more about Slidev on [documentations](https://sli.dev/).

## Demo

1. Create a new nuxt app

```bash
npx nuxi@latest init <project-name>
```

^^ Already have a project called esr-example

2. Run

```bash
npm run dev
```

3. Add storage configuration to `nuxt.config.ts`

Explain that nitro is a framework for building webservers
you could build your application to run in node
however we are going to build for cloudflare workers

```typescript
nitro: {
  preset: 'cloudflare_pages',
  storage: {
    posts: {
      driver: 'cloudflare-kv-binding',
      binding: 'Posts',
    },
  },
  devStorage: {
    posts: {
      driver: 'fs',
      base: './.data/posts'
    }
  }
}
```

4. Create some mock data in `.data/posts/1`

```json
{
  "title": "Example",
  "content": "This is an example post"
}
```


5. Create a `server/api/post/[id].get.ts` API endpoint


```typescript
export default defineEventHandler(async (event) => {
    return await useStorage().getItem(`posts:${event.context.params?.id}`)
});
```

6. Fetch the data on the front end

```vue
<script lang="ts" setup>

const { data } = await useFetch('/api/post/1');

</script>

<template>
  <div>
    <h1>Post</h1>

    {{ data }}
  </div>
</template>
```


7. Simulate an API request or slow load

```typescript
// simulate timeout
await new Promise(resolve => setTimeout(resolve, 5000));
```

8. Show refresh / pending button

```vue
<script lang="ts" setup>
const { data, refresh } = useFetch('/api/post/1');
</script>
<template>
<button @click="refresh()">refresh</button>
</template>
```

9. Build and deploy

```bash
# override this env var
CLOUDFLARE_API_TOKEN=

npm run build

npx wrangler pages deploy dist/
```


10.  Update the wrangler.toml

```toml
name="esr-example-1"
pages_build_output_dir = "dist"

[[env.production.kv_namespaces]]
binding = "Posts"
id = "6005fa3964a548bca9f839709ff8fcd0"
```
