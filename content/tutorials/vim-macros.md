---
title: 🦾 VIM Macros
description: Short explainer on VIM macro basics
date: 2022-02-26
publishDate: 2022-02-26
tags: [VIM, Macros]
showReadingTime: true
showToc: false
tocOpen: false
---

A VIM macro is just a combination of key presses that can be replayed. Let's walk through an example together.

Imagine a `javscript` file with functions, like so.

```javascript
function test1(a) {}
function tester2(a, b) {}
function testing3(a, b, c) {}
```

If we wanted to convert these function definitions to the `es6` style, we could write a macro to help us.

Here is a possible solution:

| Command            | Description                                 |
| ------------------ | ------------------------------------------- |
| `/function<ENTER>` | search for `function`                       |
| `qq`               | start recording the `q` macro               |
| `cw`               | change word (erase `function`)              |
| `const`            | insert the letters `c` `o` `n` `s` `t`      |
| `<ESC>`            | enter normal mode                           |
| `f(`               | move cursor to (find) next open parenthesis |
| `i`                | enter insert mode                           |
| `<SPACE>=<SPACE>`  | insert `=`                                  |
| `<ESC>`            | enter normal mode                           |
| `f{`               | move cursor to (find) next open curly brace |
| `i`                | enter insert mode                           |
| `=>`               | insert `=>`                                 |
| `<ESC>`            | enter normal mode                           |
| `q`                | end recording                               |

While recording the macro these changes should have happened:

```diff
-function test1(a) {};
+const test1 = (a) => {};
```

Type `n` to navigate to the next function definition and the hit `@q` to replay the recorded keystrokes (macro) again. You should end up with

```javascript
const test1 = (a) => {};
const tester2 = (a, b) => {};
function testing3(a, b, c) {}
```

Play the macro one last time to change the last function and you should be good to do.

```javascript
const test1 = (a) => {};
const tester2 = (a, b) => {};
const testing3 = (a, b, c) => {};
```

Cheers!
