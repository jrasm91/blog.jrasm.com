---
title: 🔧 TypeScript Utility Types
description: Helpful built-in utility types in TypeScript.
date: 2022-03-14
publishDate: 2022-03-14
tags: [TypeScript]
showReadingTime: true
---

[TypeScript][0] _can_ be super useful. Its type checking can reduce runtime errors during development and help solve codebase scalability challenges. Personally, I love TypeScript. At least, _most_ of the time. Occasionally I get frustrated with a failing build due to a type issue, even though the code works just fine.

Fortunately, there exists some pretty awesome [Utility Types][1], which I wish I had learned about sooner. With these built-in types, it is easier to overcome these types (no pun intended) of issues and they work better than using `any` or `unknown`.

Below are a few of my favorites.

## Record

### `Record<Keys, Type>`[^1]

Not every data structure in my code has an explicit `type` definition or a finite list of `keys`. In these situations `Record` is a nice utility that generates a dynamic type with constrains for the keys and values of an object.

```typescript
// before
const flags = {};
flags.myFeature = true;
// ✖️ Property 'myFeature' does not exist on type '{}'

// after
const flags: Record<string, boolean> = {};
flags.myFeature = true;
// ✔️ valid!
```

## Partial

### `Partial<Type>`[^2]

Make all properties of an object optional. Super useful, especially since the alternative is usually code duplication.

```typescript
// before
const updatePost = (id: number, post: Post) => { ... };
updatePost(1, { name: 'My New Name' });
// ✖ ...is missing the following properties from type 'Post': id, content.
}

// after
const updatePost= (id: number, post: Partial<Post>) => { ... };
updatePost(1, { name: 'Twitter Post #1' });
// ✔️ valid!
```

## Inferred

### `Parameters`[^3] `ConstructorParameters`[^4] `ReturnType`[^5]

This is perfect for when a type definition doesn't exist or can't otherwise be imported.

```typescript
// some-package/index.d.ts
type InternalOptions = ...; // not exported!
type InternalResults = ...;  // not exported!
export function config(options: InternalOptions) : InternalResults;
```

```typescript
// app.ts
import { config } from 'some-package';
type ConfigOptions = Parameters<typeof config>[0];
const myConfig: ConfigOptions = { ... };
// ✔️ valid!

type Results = ReturnType<typeof config>;
let myResult: Results;
myResult = config(myConfig);
// ✔️ valid!
```

## Conclusion

These are the utilities that I use most frequently and they make it more convenient to work with TypeScript. I recommend reading through then [entire list][1] and seeing what built-in types could simplify _your_ life.

[0]: https://www.typescriptlang.org/
[1]: https://www.typescriptlang.org/docs/handbook/utility-types.html

[^1]: [TypeScript Utility Types: Record](https://www.typescriptlang.org/docs/handbook/utility-types.html#recordkeys-type)
[^2]: [TypeScript Utility Types: Partial](https://www.typescriptlang.org/docs/handbook/utility-types.html#partialtype)
[^3]: [TypeScript Utility Types: Parameters](https://www.typescriptlang.org/docs/handbook/utility-types.html#parameterstype)
[^4]: [TypeScript Utility Types: ReturnType](https://www.typescriptlang.org/docs/handbook/utility-types.html#returntypetype)
[^5]: [TypeScript Utility Types: ConstructorParameters](https://www.typescriptlang.org/docs/handbook/utility-types.html#constructorparameterstype)
