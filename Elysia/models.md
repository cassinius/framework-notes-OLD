* Model re-mapping

You should be able to do something like this:

```js
const a = new Elysia()
	.model({
		sign: t.Object({
			username: t.String(),
			password: t.String()
		})
	})
	.model(({ sign }) => ({
		signWithPagination: t.Object({
			results: sign,
			page: t.Number()
		})
	}))
```

Then you can just use the reference model in there:

```js
const app = new Elysia()
	.use(a)
	.post('/sign-in', ({ body }) => body, {
		body: 'signWithPagination'
	})
	.listen(3000)
```
