# Elysia

## Elysia performance tricks

### property injection (context, ctx props)

Basically how it works is that Elysia can read your code and analyze which property is required, then inject the code. You can think of this as a lazy getter. If a property is called, then it will be initialized, otherwise, it won't.

If the whole context is passed, then every property will be created, even if it's not used. Basically, that's how Elysia works, and why Elysia is fast.

So to resolve this, you can create a function that only accepts what's needed. Hope this answer some of your questions.

## Elysia (app) types

### Mixing / combining Elysia app types

* This works:
```js
import { Elysia, t } from 'elysia'

const app1 = new Elysia()
    .get('/a', () => 'a')
    .listen(3000)

const app2 = new Elysia()
    .get('/b', () => 'b')
    .listen(3000)

export type App = typeof app1 & typeof app2

type Routes = keyof App['schema'] // return /a | /b
```
* This doees not (because of the `prefix`):
```js
import { Elysia } from 'elysia';

const app1 = new Elysia({ prefix: '/a' }).get('', () => 'a');

const app2 = new Elysia({ prefix: '/b' }).get('', () => 'b');

export type App = typeof app1 & typeof app2; // never

type Routes = keyof App['schema']; // string | number | symbol
```

### Generating a `d.ts` file

* need to have this at the end of your file
```js
export type App = typeof app;
```
* then generation via `tsc -d` should work...

### Hooks for route groups

```js
app.group('/:category', (app) => 
    app
      .onBeforeHandle([isAuthenticated, doesCategoryExist])
      .get('/:id', () => {
         // I know I'm safe
      })
)
```

### Re-naming and prefixing plugins in ctx

```js
// this would be a plugin provided by a third party
const myPlugin = (app: Elysia) => app.decorate('myProperty', 42);

new Elysia()
  .use(
    myPlugin
      .mapContext({
        myProperty: 'prop' // rename derived or decorated properties one by one
      })
      .prefixAll('my-') // and/or apply a prefix to all
  )
  .get('/', (ctx) => ctx['my-prop'])
  .listen(8080);
```

