---
title: 'VIM Commands'
description: A list of VIM commands that I have learned, since picking up VIM in 2021.
date: 2022-02-26
publishDate: 2022-02-26
tags: [VIM]
showReadingTime: false
showToc: true
tocOpen: true
---

### Navigation

| Command | Description                                           |
| ------- | ----------------------------------------------------- |
| `h`     | move cursor left                                      |
| `l`     | move cursor right                                     |
| `k`     | move cursor up                                        |
| `j`     | move cursor down                                      |
| `b`     | move cursor to start of _previous_ word               |
| `w`     | move cursor to start of _next_ word                   |
| `e`     | move cursor to _end_ of _next_ word                   |
| `gg`    | move cursor to _top_ of file                          |
| `G`     | move cursor to _bottom_ of file                       |
| `fx`    | move cursor to _next_ occurrence of character `x`     |
| `Fx`    | move cursor to _previous_ occurrence of character `x` |
| `{`     | move cursor up a code block                           |
| `}`     | move cursor down a code block                         |
| `zz`    | move current line to middle of screen                 |

### Editing

| Command | Variation | Description                                                             |
| ------- | --------- | ----------------------------------------------------------------------- |
| `i`     |           | insert mode before current character                                    |
| `I`     |           | insert mode at beginning of line                                        |
| `O`     |           | new line above                                                          |
| `o`     |           | new line below                                                          |
| `a`     |           | enter insert mode with cursor after current character                   |
| `A`     |           | enter insert mode with cursor at the end of the line                    |
| `S`     | `dd`      | delete current line and go to insert mode                               |
| `cw`    | `dw`      | change to end of word (delete from current to end of word)              |
| `ciw`   | `diw`     | change in word (delete whole word, with cursor anywhere in the word)    |
| `cit`   | `dit`     | change in tag (delete current word and go to insert mode)               |
| `cix`   | `dit`     | change in `x` (delete from cursor to left and right until seeing `x`)   |
| `ctx`   | `dtx`     | change to `x` (delete from current location up until the character `x`) |

### Selection

| Command | Description             |
| ------- | ----------------------- |
| `v`     | visual mode             |
| `V`     | visual mode (full line) |

### Copy/Paste

| Command | Description                                         |
| ------- | --------------------------------------------------- |
| `p`     | paste on new line below                             |
| `P`     | paste on new line above                             |
| `yit`   | yank (copy) in tag                                  |
| `"+y`   | yank (copy) to system clipboard                     |
| `"xY`   | yank (copy) to `x` buffer (x can be almost any key) |
| `"xp`   | paste contents of `x` buffer                        |

### Search

| Command | Description       |
| ------- | ----------------- |
| `/`     | enter search mode |
| `n`     | next result       |
| `N`     | previous result   |

### Macros

| Command | Description                       |
| ------- | --------------------------------- |
| `qq`    | start recording for the `q` macro |
| `q`     | stop recording                    |
| `@q`    | play the `q` macro                |

### Other

| Command | Description          |
| ------- | -------------------- |
| `.`     | do last action again |
