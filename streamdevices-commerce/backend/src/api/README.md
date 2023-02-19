# Custom endpoints

You may define custom endpoints by putting files in the `/api` directory that export functions returning an express router.
```js
import { Router } from "express"

export default () => {
  const router = Router()

  router.get("/products", (req, res) => {
    res.json({
      message: "Welcome to Stream Devices!"
    })
  })

  return router;
}
```

A global container is available on `req.scope` to allow you to use any of the registered services from the core, installed plugins or your local project:
```js
import { Router } from "express"

export default () => {
  const router = Router()

  router.get("/products", async (req, res) => {
    const productService = req.scope.resolve("productService")

    const [product] = await productService.list({}, { take: 1 })

    res.json({
      message: `Welcome to ${product.title}!`
    })
  })

  return router;
}
```
