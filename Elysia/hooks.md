* Re-usable local hook attempt (from gh issues, not reproduced)

```js
export const nodeMiddlewares = new Elysia({ name: "node@middlewares" })
  .use(nodeModel)
  .guard({ body: "node.dto" })
  .derive(({ set, body, params }) => {
    const validateBody = () => {
      const { name, userId } = body;
      if (!name) {
        set.status = 404;
        throw new NotFoundError("Please provide the name!");
      }
      if (!userId) {
        set.status = 404;
        throw new NotFoundError("Unknown node owner!");
      }
    };
    const isIntParams = () => {
      const { id } = params;
      const regex = new RegExp(/[0-9]/);
      if (!regex.test(id)) {
        set.status = 400;
        throw new ParseError("Invalid params type!");
      }
    };
    return { validateBody, isIntParams };
  });

// After that, you just inject it into the instance you want and declare it like this:

import { Elysia } from "elysia";
import { nodeMiddlewares } from "$middlewares";
import { nodeControllers } from "$controllers";

export const node = new Elysia({ name: "node@routes" })
  .use(nodeControllers)
  .use(nodeMiddlewares)
  .get("/nodes", ({ getNodes }) => getNodes())
  .group("/node", (node) =>
    node
      .post("/", ({ createNode }) => createNode(), {
        beforeHandle: ({ validateBody }) => validateBody(),
      })
      .put("/:id", ({ updateNode }) => updateNode(), {
        beforeHandle: [
          ({ isIntParams }) => isIntParams(),
          ({ validateBody }) => validateBody(),
        ],
    // The rest of the code
```
