---
title: Personal Cheatsheet
summary: For all those things I have to lookup over and over.
created: 2022-02-02
updated: 2022-02-02
tags: [Linux, Ubuntu, Docker, Git, Hugo, Networking, Bash]
showReadingTime: false
showToc: true
tocOpen: true
---

### Linux / Ubuntu

#### Networking

Restart network manager (reset DNS cache)

```bash
  sudo /etc/init.d/network-manager restart
```

#### SSH

Fix ssh key permissions

```bash
chmod 400 ./key.pem
```

Copy from local to remove

```bash
scp -i key.pem ~/path/to/source user@remote:~/path/to/destination
```

Copy from remote to local

```bash
scp -i key.pem user@remote:~/path/to/source ~/path/to/destination
```

### Development
