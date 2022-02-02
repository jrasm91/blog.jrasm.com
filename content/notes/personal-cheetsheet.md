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

### Filesystem

View mounts and available space

```bash
df -h
```

### .bashrc

History

```bash
HISTSIZE=10000
HISTFILESIZE=20000
```

PS1

Show git branch (important part is `$(__git_ps1)` wrapped in red escape)

```
PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\W\[\033[00m\]\[\e[91m\]$(__git_ps1)\[\e[00m\]$ '
```

Aliases

```bash
alias new-password="openssl rand -base64 32"     # random characters
alias dev="npm run start:dev"                    # dev => npm run start:dev
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

### Git

```
git config --global user.name "John Doe"
git config --global user.email john@doe.com
git config --global core.editor vim
git config --global log.date relative
git config --global format.pretty format:%C(yellow)%h %Cblue%>(14)%ad %Cgreen%<(16)%aN%Cred%d %Creset%s
```
