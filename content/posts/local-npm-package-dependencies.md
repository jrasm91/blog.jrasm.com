---
title: '📦 Local NPM Dependencies'
description: How to use local npm packages as dependencies in other projects.
date: 2022-03-07
publishDate: 2022-03-07
tags: [Tutorial, JavaScript, Package Manager]
showReadingTime: true
showToc: false
tocOpen: false
---

This is a quick overview of two different ways to use local packages as dependencies to other node projects installed on the same machine.

Assume we have the following folder structure:

```text
my-app/
├── api/
│   ├── package.json
│   ├── dist/
│   └── src/
│       └── index.ts
└── common/
    ├── package.json
    ├── dist/
    └── src/
        └── index.ts
```

If we are developing or testing the `api` package, and would like to replace the `common` dependency with our local `common` package, there are a few ways we successfully override this dependency.

## 1. npm install

```bash
npm install <package>
```

The easiest way to do this is with the `npm install` command. According to the [npm install docs](https://docs.npmjs.com/cli/v8/commands/npm-install) we can pass a few different `<package>` identifiers, such as a **folder**, tarball file, tarball url, git url, or a github project. Using a relative folder path, we can install the `common` folder as a dependency via:

```bash
cd api
npm i ../common
```

Under the hood this command creates a symlink for `common`, linking to the local folder.

```text
my-app/
└── api/
    └── node_modules/
        └── common -> ../../common/
```

## 2. npm link

This command has a very similar outcome to the above method, however the process is a little different. It takes two steps:

1. run `npm link` in the `common` package

```bash
cd common
npm link
```

2. run `npm link common` in the `api` package

```bash
cd api
npm link
```

The first command creates a symlink in the global context (`node_modules` for the user). For example:

```text
/home/user/
└── node_modules/
    └── common -> /home/user/projects/my-app/common/
```

The second command creates a symlink from the local context to the global one. For example:

```text
my-app/
└── api/
    └── node_modules/
        └── common -> /home/user/node_modules/common
```

Now `my-app/api/node_modules/common` points to `my-app/common` via two symlinks. At anytime the symlinks can be removed via:

```bash
cd my-app
npm uninstall common            # remove local symlink
npm uninstall --global common   # remove global symlink
```
