---
title: Development Cheatsheet
description: What I inevitably lookup over and over.
date: 2022-02-02
publishDate: 2022-02-26
tags: [Docker, Git, SQLite]
showReadingTime: false
showToc: true
tocOpen: true
---

### Node

Executable file ("hashbang" indicator)

```
#!/usr/bin/env node
```

### Docker

Tail logs

```bash
docker logs <CONTAINER> --follow
docker logs <CONTAINER> --follow --since 1m
docker logs <CONTAINER> --follow --since 5m
docker logs <CONTAINER> --follow --since 1h
```

### SQLite

```sqlite
.tables       # list tables
.mode column  # display in columns
.headers on   # show column headers
```

### Git

```
git config --global user.name "John Doe"
git config --global user.email john@doe.com
git config --global core.editor vim
git config --global log.date relative
git config --global format.pretty format:%C(yellow)%h %Cblue%>(14)%ad %Cgreen%<(16)%aN%Cred%d %Creset%s
```
