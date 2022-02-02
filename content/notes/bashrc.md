---
title: .bashrc
summary: Useful snippets for .bashrc files
created: 2022-02-02
updated: 2022-02-02
tags: [Bash, Alias, Password, .bashrc]
showReadingTime: false
showToc: false
tocOpen: true
---

### History

```bash
HISTSIZE=10000
HISTFILESIZE=20000
```

### PS1

Show git branch (important part is `$(__git_ps1)` wrapped in red escape)

```
PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\W\[\033[00m\]\[\e[91m\]$(__git_ps1)\[\e[00m\]$ '
```

### Aliases

```bash
alias new-password="openssl rand -base64 32"     # random characters
alias dev="npm run start:dev"                    # dev => npm run start:dev
```
