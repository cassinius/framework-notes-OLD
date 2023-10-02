## Typebox notes

* Allow for 
```js
params: t.Object({
  item_id: t.String()
}, { additionalProperties: true })
```

* Default field
```js
email: t.String({
	default: "",
	format: "email"
})
```