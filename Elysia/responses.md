* Readable stream

```js
app.get(
  '/',
  () =>
    new Response(
      new ReadableStream({
        pull(controller) {
          controller.enqueue('Hello world!');

          controller.close();
        }
      })
    )
);
```