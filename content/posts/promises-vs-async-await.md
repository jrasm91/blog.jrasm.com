---
title: '⚔️ Promises vs async/await'
description: An overview of the interoperability between Promises and async/await in TypeScript.
date: 2023-11-07
publishDate: 2023-11-07
tags: [TypeScript, Async/Await, Promises]
showReadingTime: true
showToc: false
tocOpen: false
---

A long time ago, before [Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) existed, we had callbacks, callback hell, and some insane code and libraries to deal with the mess they created.

Luckily, we have moved on to better times. With the modernization of the Web, [ES6 Features]({{< ref "/posts/top-es6-features" >}}), etc. promises have become first class citizens and part of the standard library.

Along with promises came [async][async]/[await][await]. In my opinion, this has improved code _readability_ essentially without changing them semantics of the code.

## Syntactic Sugar

> In computer science, syntactic sugar is syntax within a programming language that is designed to make things easier to read or to express. It makes the language "sweeter" for human use: things can be expressed more clearly, more concisely, or in an alternative style that some may prefer.
> — [Wikipedia][1]

This exactly describes the relationship between async/await and promises. In practice any asynchronous code can be written as (1) promises, (2) async/await, or (3) a combination of the two. Without a fundamental understanding of promises it will always be a little bit difficult to understand exactly how the code execute in some of the trickier situations.

## Examples

Here's a few examples of how code can be written with promises vs async/await

### Try / Catch

In this example you can see how a `.then().catch().finally()` can be converted to standard `try/catch` syntax.

```typescript
// promises
const main = () => {
  return axios
    .post('/message', { data: 'Hello' })
    .then(({ status, data }) => console.log('Sent message'))
    .catch((error) => console.error('Unable to send message', error))
    .finally(() => console.log('Done'));
};
```

```typescript
// async/await
const main = async () => {
  try {
    const { status, data } = await axios.post('/message', { data: 'Hello' });
    console.log('Sent message');
  } catch (error) {
    console.error('Unable to send message', error);
  } finally {
    console.log('Done');
  }
};
```

### Multiple Async Tasks

In this example you can see how much nicer/cleaner it is to write sequential operations using async/await. Specifically with promises it can be difficult to execute sequential steps while accumulating the results.

```typescript
// promises
const main = () => {
  axios
    .post('/message', { data: 'Hello' })
    .then((message1) => {
      const message2 = axios.post('/message', { data: 'Hello' });
      return [message1, message2];
    })
    .then(([message1, message2]) => console.log(message1, message2));
};
```

```typescript
// async/await
const main = async () => {
  const message1 = await axios.post('/message', { data: 'Hello 1' });
  const message2 = await axios.post('/message', { data: 'Hello 2' });
  console.log(message1, message2);
};
```

[1]: https://en.wikipedia.org/wiki/Syntactic_sugar
[async]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/async_function
[await]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await
