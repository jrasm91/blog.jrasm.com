---
title: Linux/Ubuntu Cheatsheet
description: All those I cannot seem to remember.
date: 2022-02-02
publishDate: 2022-02-26
tags: [Linux, Ubuntu, Networking, Bash, DNS]
showReadingTime: false
showToc: true
tocOpen: true
---

### Networking

Restart network manager (reset DNS cache)

```bash
sudo /etc/init.d/network-manager restart
```

Ports that are listening

```bash
sudo lsof -i -P -n | grep LISTEN
```

Process listening on a specific port

```bash
sudo lsof -i:3000
```

Search by process name

```bash
pgrep -a node
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

View folder size in current directory

```bash
du -d 1
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
