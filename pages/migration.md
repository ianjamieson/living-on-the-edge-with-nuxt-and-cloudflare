---
---
<NovaMantis></NovaMantis>
# incremental migration


<!-- ```toml {all|3}
[env.production]
routes = [
    "tixel.com/au/tickets/event-1"
]
``` -->

````md magic-move
```toml {*}
[env.production]
routes = [
    "tixel.com/au/tickets/2024/event-1"
]
```

```toml {*}
[env.production]
routes = [
    "tixel.com/au/tickets/2024/event-1",
    "tixel.com/nz/tickets/*"
]
```
````

<!--
- our event page was already live with many complex features for specific events
- we could use wrangler.toml file to specify routes to redirect to workers
-  -->