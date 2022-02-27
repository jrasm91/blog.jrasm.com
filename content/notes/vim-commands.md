---
title: 'VIM Commands'
summary: VIM commands that I am familiar with.
created: 2022-02-26
updated: 2022-02-26
tags: [VIM]
showReadingTime: false
showToc: true
tocOpen: true
---

### Navigation

| Command | Description                                                |
| ------- | ---------------------------------------------------------- |
| `h`     | left                                                       |
| `l`     | right                                                      |
| `j`     | up                                                         |
| `b`     | start of previous word                                     |
| `w`     | start of next word                                         |
| `e`     | end of next word                                           |
| `gg`    | go to top of file                                          |
| `G`     | go to bottom of file                                       |
| `zz`    | move current line to middle of screen                      |
| `fx`    | move current (find) _next_ occurrence of character `x`     |
| `Fx`    | move current (find) _previous_ occurrence of character `x` |
| `zz`    | move current line to middle of screen                      |

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
