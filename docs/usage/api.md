---
layout: docs
title: API
description: How to use the Node.js API.
permalink: /docs/usage/api/
---

```javascript
var to5 = require("6to5");
```

## to5.transform(code, [[options](/docs/usage/options)])

Transforms the passed in `code`. Returning an object with the generated code,
source map, and AST.

```js
to5.transform(code, [options]) // => { code, map, ast }
```

**Example**

```js
var result = to5.transform("code();", options);
result.code;
result.map;
result.ast;
```

## to5.transformFile(filename, [[options](/docs/usage/options)], callback)

Asynchronously transforms the entire contents of a file.

```js
to5.transformFile(filename, [options], callback)
```

**Example**

```js
to5.transformFile("filename.js", options, function (err, result) {
  result; // => { code, map, ast }
});
```

## to5.transformFileSync(filename, [[options](/docs/usage/options)])

Synchronous version of `to5.transformFile`. Returns the transformed contents of
the `filename`.

```js
to5.transformFileSync(filename, [options]) // => { code, map, ast }
```

**Example**

```js
to5.transformFileSync("filename.js", options).code;
```
