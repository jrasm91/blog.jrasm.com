---
title: 🐳 Sharing Code in Docker Builds
date: 2021-04-02
publishdate: 2021-04-02
cover:
  image: images/logos/docker.png
  caption: Docker
  responsiveImages: true
  hiddenInList: true
tags: [Docker, Dockerfile, .dockerignore, TypeScript]
---

Docker is great. But also, it can be a pain to work with sometimes. Today was one of those days. I had a pretty simple project with a frontend and a backend, both written in [TypeScript][0]. The two projects had some common interfaces that I wanted to share between the two projects.

Locally, I had my code setup like this:

```
api/
  src/
    models/
      model1.ts
      index.ts

frontend/
  src/
    app/
      models/
        model1.ts <-- Copy
        index.ts
```

I wanted to share all the models between the `api` and the `frontend`. I accomplished this by deleting the copied models from `frontend` and replacing `models/index.ts` with:

```
export * from '../../../../api/src/models'
```

Nothing changed for the `api`, but now the `frontend` (Angular) no longer needed it's own copy of the models.

Locally this worked great. Building the `api` with `tsc` worked, no problem️. Building the `frontend` with `ng build --prod` also worked, no problem️.

## Building with Docker

I needed to build two separate docker images, one for the `api` (`node-alpine`) and one for the `frontend` (`nginx`). I had a `Dockerfile` in each folder:

```
api/
  src/
  Dockerfile

frontend/
  src/
  Dockerfile
```

The `Dockerfile` for the `api` was a typical `Node.js` build:

```dockerfile
FROM node:12-alpine as BUILD

RUN apk --no-cache add python make g++

COPY package*.json ./
RUN npm ci

COPY ts*.json ./
COPY src/ ./src/
RUN npm run build
RUN npm prune --production

FROM node:12-alpine

WORKDIR /usr/src/api
COPY --from=BUILD node_modules node_modules
COPY --from=BUILD dist dist
COPY --from=BUILD package.json package.json
COPY --from=BUILD package-lock.json package-lock.json

ENV NODE_ENV production
ENV PORT 4201
ENV NO_COLOR true

EXPOSE 4201

CMD [ "npm", "start" ]

```

The `Dockerfile` for the `frontend` was a typical `nginx` build:

```dockerfile
FROM node:12-alpine AS BUILD

WORKDIR /usr/src/frontend

COPY frontend/package*.json ./

RUN npm ci

COPY browserslistrc angular.json ts*.json ./
COPY src ./src

RUN npm run build

FROM nginx:1.19-alpine

COPY --from=BUILD /usr/src/frontend/dist /usr/share/nginx/html
COPY frontend/nginx.conf /etc/nginx/nginx.conf
```

This is where I started running into problems.

## No Exported Member

I tried to build the image by running:

```bash
docker build .
```

Buuuuuuuuut, the shared models weren't being included in the build context or copied to the build image, leading to errors like this:

```bash
Error: src/app/auth/auth.service.ts:6:10 - error TS2305: Module '"../models"' has no exported member 'Model1'.
6 import { Model1 } from '../models';

```

This can be fixed by running the command with `..` instead of `.`, which will send both the `api` and `frontend` files to the `docker` build context, and subsequently make the api models available.

## Docker Build Context

I updated the command and tried again.

```bash
docker build ..
```

Buuuuuuuuut, then I got this error:

```
unable to prepare context: unable to evaluate symlinks in Dockerfile path: lstat /home/.../Dockerfile: no such file or directory
```

Basically, now `docker` is looking for a `Dockerfile` at `..` instead of `frontend`. Great. 🤦‍♂️

I fixed this by specifying the path to the `Dockerfile` with the `-f` switch:

## .dockerignore

I updated the command and tried, _again_.

```bash
docker build -f Dockerfile ..
```

Now that the build was finally starting to work, I noticed another problem:

```bash
Sending build context to Docker daemon  812.8MB <---
Step 1/10 : FROM node:12-alpine AS BUILD
...
```

It was sending close to `1GB` of data to the build context. There was a `.dockerignore` file, but it was in `frontend`. Since I moved the build context up one level, I needed to move the `.dockerignore` up as well.

## Dockerfile `COPY`

OK. I updated the `.dockerignore` location:

```txt
api/
  Dockerfile
  .dockerignore

frontend/
  Dockerfile

.dockerignore <-- Moved from frontend/
```

Everything was pretty much working as expected now, except that I needed to update the `Dockerfile` to copy from the new paths. I.e.

```dockerfile
...
COPY frontend/package*.json
...
COPY frontend/.browserslistrc frontend/angular.json frontend/ts*.json ./
COPY frontend/src ./src
..
COPY frontend/nginx.conf /etc/nginx/nginx.conf
```

All of the `COPY` commands needed to include the `frontend/` prefix.

Finally, I also needed to copy the `api` models via:

```dockerfile
COPY api/src/models /usr/src/api/src/models
```

Since I was using the build context of `api/ + frontend/`, copying the `api/` models worked no problem.

## Success! 🎉

After updating:

0. The build context
1. `Dockerfile` argument
2. `.dockerignore` path
3. `docker COPY` paths

and including the `api` models, I was finally able to get a successful build.

And all this to share some TypeScript interfaces... 😂

[0]: https://www.typescriptlang.org/
