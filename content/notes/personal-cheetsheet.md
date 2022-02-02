---
title: Personal Cheatsheet
summary: For all those things I have to lookup over and over.
created: 2022-02-02
updated: 2022-02-02
tags: [Linux, Ubuntu, Docker, Git, Networking, Bash, DNS, SQLite]
showReadingTime: false
showToc: true
tocOpen: true
---

## Linux / Ubuntu

### Networking

Restart network manager (reset DNS cache)

```bash
  sudo /etc/init.d/network-manager restart
```

### Cryptography

Print a x509 certificate

```bash
openssl x509 -in public.pem -text
```

### SSH

Fix ssh key permissions

```bash
chmod 400 ./key.pem
```

Copy from local to remove

```bash
scp -i key.pem ~/path/to/src user@remote:~/path/to/dest
```

Copy from remote to local

```bash
scp -i key.pem user@remote:~/path/to/src ~/path/to/dest
```

## Development

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
