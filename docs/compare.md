---
layout: docs
title: Compare
description: Differences between 6to5 and other ES6 transpilers.
permalink: /docs/compare/
redirect_from: /differences.html
---

## Differences

### Readable code

The fundamental concept behind 6to5 is that the generated code must be close as
possible to the original, retaining all the same formatting and readability.

Many other transpilers are just concerned with making the code work while 6to5
is concerned with making sure it works **and** is readable at the same time.

For example, given the following array comprehension:

```js
var seattlers = [for (c of customers) if (c.city == "Seattle") { name: c.name, age: c.age }];
```

is generated to the following with 6to5:

```js
var seattlers = Array.from(customers).filter(function (c) {
  return c.city == "Seattle";
}).map(function (c) {
  return {
    name: c.name,
    age: c.age
  };
});
```

The following is what Traceur generates:

```js
var seattlers = (function() {
  var c;
  var $__20 = 0,
      $__21 = [];
  for (var $__22 = customers[$traceurRuntime.toProperty(Symbol.iterator)](),
      $__23; !($__23 = $__22.next()).done; ) {
    c = $__23.value;
    if (c.city == "Seattle")
      $traceurRuntime.setProperty($__21, $__20++, {
        name: c.name,
        age: c.age
      });
  }
  return $__21;
}());
```

As you can tell, it's not very pretty. Instead of mapping directly to a runtime,
like other transpilers, 6to5 maps directly to the equivalent ES5.

Sometimes there are little inline functions that 6to5 needs. These are
placed at the top of your file much like coffee-script does. If these
bother you then you can use the [optional runtime](/docs/usage/runtime).
We promise that these inline functions will never be significant and will
always be used as little as possible.

### Static analysis

6to5 uses a lot of static analysis to simplify code as much as possible.
Not many other transpilers do this, and those that do don't do it nearly
as much as 6to5. This process is pretty intensive but it leads to higher
quality code.

### Spec compliancy

6to5 prides itself on
[spec compliancy](https://kangax.github.io/compat-table/es6/). We have
excellent support for edgecases, something that many other transpilers
suffer from, including Traceur. When you use 6to5 you can be confident
that when you turn it off and use your code in a full ES6 environment
**it'll just work**.

## Comparison to other transpilers

### Features

|                              | 6to5 | Traceur | Typescript | es6-transpiler | es6now | jstransform |
| ---------------------------- | ---- | ------- | ---------- | -------------- | ------ | ----------- |
| Source maps                  | ✓    | ✓       | ✓          |                |        | ✓           |
| No compiler global pollution | ✓    |         | ✓          | ✓              |        | ✓           |
| Optional/no runtime          | ✓    |         | ✓          | ✓              |        | ✓           |
| Browser compiler             | ✓    | ✓       | ✓          |                |        |             |

### Language Support

|                              | 6to5 | Traceur | Typescript | es6-transpiler | es6now | jstransform |
| ---------------------------- | ---- | ------- | ---------- | -------------- | ------ | ----------- |
| Abstract references          | ✓    |         |            |                |        |             |
| Array comprehension          | ✓    | ✓       |            | ✓              |        |             |
| Arrow functions              | ✓    | ✓       | ✓          | ✓              | ✓      | ✓           |
| Async functions              | ✓    | ✓       |            |                |        |             |
| Async generator functions    | ✓    | ✓       |            |                |        |             |
| Classes                      | ✓    | ✓       |            | ✓              | ✓      | ✓           |
| Computed property names      | ✓    | ✓       |            | ✓              | ✓      |             |
| Constants                    | ✓    | ✓       |            | ✓              |        |             |
| Default parameters           | ✓    | ✓       | ✓          | ✓              | ✓      |             |
| Destructuring                | ✓    | ✓       |            | ✓              | ✓      | ✓           |
| Exponentiation operator      | ✓    | ✓       |            |                |        |             |
| For-of                       | ✓    | ✓       |            | ✓              | ✓      |             |
| Generators                   | ✓    | ✓       |            |                |        |             |
| Generator comprehension      | ✓    | ✓       |            |                |        |             |
| JSX                          | ✓    |         |            |                |        |             |
| Let scoping                  | ✓    | ✓       |            | ✓              |        |             |
| Modules                      | ✓    | ✓       |            |                | ✓      |             |
| Object rest/spread           | ✓    |         |            |                |        | ✓           |
| Property method assignment   | ✓    | ✓       |            | ✓              | ✓      | ✓           |
| Property name shorthand      | ✓    | ✓       | ✓          | ✓              | ✓      | ✓           |
| Rest parameters              | ✓    | ✓       | ✓          | ✓              | ✓      | ✓           |
| React                        | ✓    |         |            |                |        |             |
| Spread                       | ✓    | ✓       |            | ✓              | ✓      |             |
| Template literals            | ✓    | ✓       |            | ✓              | ✓      | ✓           |
| Types                        | ✓    | ✓       | ✓          |                |        | ✓           |
| Unicode regex                | ✓    | ✓       |            | ✓              |        |             |
