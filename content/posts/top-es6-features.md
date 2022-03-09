---
title: 🥇 Top ES6 Features
description: A few of my favorite ES6 features.
date: 2022-03-08
publishDate: 2022-03-08
tags: [JavaScript, ES6]
showReadingTime: true
showToc: true
tocOpen: true
---

## Arrow Functions

Arrow functions are a compact alternative to traditional function expression. They also do not require rebinding `this`. See [mdn](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) for more details.

In my opinion, `this` is one of the more tricky JavaScript concepts to grasp. It is often unintuitive and that inevitably leads to unexpected behavior. If nothing else, arrow functions usually make `this` more intuitive, leading to less error-prone code.

```javascript
// Traditional
function foo() {
  console.log('Hi Mom!');
}
[1, 2, 3].map(function (x) {
  return x + 1;
});

// Arrow Functions
const foo = () => {
  console.log('Hi Mom!');
};
const foo = () => console.log('Hi Mom!');
[1, 2, 3].map((x) => x + 1);
```

## Destructuring Assignment

This is one of my favorite features, because it leads to clean, concise code that is easy to read. It comes in a few different flavors.

### Object

Allows for multiple assignments in a single line.

```javascript
// before
function handler(req, res) {
  const page = req.query.page;
  const size = req.query.size;
  const filter = req.query.filter;
}

// after
function handler(req, res) {
  const { page, size, filter } = req.query;
}
```

### Array

Same as above, but for arrays.

```javascript
// before
function handler(req, res) {
  const parts = req.headers.authorization.split(':');
  const key = parts[0];
  const value = parts[1];
}

// after
function handle(req, res) {
  const [key, value] = req.headers.authorization.split(':');
}
```

### Imports

Object destructuring, just with import statements.

```javascript
// before
import * as utils from './utils';

async function handle() {
  await utils.sleep(3);
}

// after
import { sleep } from './utils';

async function handle() {
  await sleep(3);
}
```

Or, the `CommonJS` equivalent.

```javascript
// before
const utils = require('utils');

async function handle() {
  await utils.sleep(3);
}

// after
const { sleep } = require('utils');

async function handle() {
  await sleep(3);
}
```

## Property Shorthand

This is another feature that has removed a lot of duplicate code for me. If the object `key` and `value` variable name are same, you can use this simplified syntax.

```javascript
// before
function handler(req, res) {
  const page = req.query.page;
  const size = req.query.size;
  const filter = req.query.filter;
  const options = {
    page: page,
    size: size,
    filter: filter,
  };
  return res.send(service.search(data, options));
}

// after
function handle(req, res) {
  const { page, size, filter } = req.query;
  const options = { page, size, filter }; // <-- simplified syntax
  return res.send(service.search(data, options));
}

// after (simplified)
function handle(req, res) {
  const { page, size, filter } = req.query;
  return res.send(service.search(data, { page, size, filter })); // <-- inline
}
```

I especially like this shorthand approach, because resulting lines can often be further reduced. In this example, `options` becomes small enough to inline.

## Template Literals

This is a great quality of life feature, allowing multiline strings with interpolation. Especially with longer, more complex string generation, this can make the code a lot cleaner.

```javascript
// before
function onRegistration(user) {
  const email = user.email;
  const uid = user.uid;
  slack.send(':rocket: New user! *email*=' + email + ',*uid*=' + uid);
}

// after
function onRegistration(user) {
  const { email, uid } = user;
  slack.send(`:rocket: New user! *email*=${email},*uid*=${uid}`);
}
```

I quickly got tired of converting existing strings from single quotes to backticks, but there's actually a VSCode extension specifically for this called [Template String Converter](https://marketplace.visualstudio.com/items?itemName=meganrogge.template-string-converter). It automatically converts surrounding single or double quotes to backticks when `${` is typed! 🎉
