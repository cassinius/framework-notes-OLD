# "Old" pages vs. app router

> *"Rendering is usually not the bottleneck for your app performance"*

- (at least in combination with heavy data fetching...)

## Pages

> *"ISR - Incremental Static Regeneration"*

* You use special functions like `getServerSideProps` for data fetching
  - and inject them into the *client* component returning them as props 
* There is only `1 caching operation` permissible per route
  * you cache the whole route or you don't cache anything
* This makes pages as slow as the slowest data fetching operation (ISR)
* Plus: *hydration for everything*
* Plus: re-fetching ALL the data on the client

## App router

> "*granular caching of ANY async call"*

* `Async components` can now run on the server
  - no endpoint / component segregation anymore
  - not sure how it renders / hydrates in this model (is there client-side fetching after the first run / re-render??)
* You write normal `async / await` fetching code
  - then just assign the result to a variable
* In this model, *any fetch can be `cached` on it's own*
* This makes the route as slow as the slowest *uncachable* data fetching operation
* Plus: *partial hydration* !?
* Plus: only partial re-fetching on the client (*islands* ... !?)

![Theos_note](pages_vs_app_router.png)
