---
title: 'Local Npm Packages'
date: 2021-05-03T17:32:46-07:00
draft: true
tags: [Docker, Typescript]
---

In a recent post I talked about [Sharing code in docker builds][0]. After using this solution for awhile, I become aware of some other annoying consequences of that particular solution.

The biggest problem was the extra nesting in the `dist` folder.

For example, the compiled output for `api` in this project structure:

```
project/
  common/
    ...
  api/
    ...
  frontend/
    ...
```

becomes...

```
project/
  api/
    dist/
      api/
        ...
      common/
        ...
```

Since some of the `common` files are referenced in `api` the output changes dramatically, in order for the relative imports to still resolve correctly. The causes a few problems. The biggest ones for me were:

0.  Output references in `package.json` are wrong.

```diff
{
+ "main": "dist/api/src/index.js"
- "main": "dist/index.js"
}
```

1.  Relative files are wrong.

```diff
+ fs.readFile('../../../config.json')`
- fs.readFile('../config.json')`
```

[0]: /posts/sharing-code-in-docker-builds

```

```
