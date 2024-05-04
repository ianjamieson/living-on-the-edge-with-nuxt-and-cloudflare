---
layout: center
---
<NovaMantis></NovaMantis>

# demo


<!--
1. Create a new nuxt app

```bash
npx nuxi@latest init <project-name>
```

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
  storage: {
    posts: {
      // prod config
    }
  },
  devStorage: {
    posts: {
      driver: 'fs',
      base: './.data/posts'
    }
  }
}
```

1. Create some mock data in `.data/posts/1`

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
-->