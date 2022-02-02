---
title: 🛠 Fixing VSCode Shell Environment
date: 2021-03-25
publishdate: 2021-03-25
tags: [VSCode, Shell, Startup Application]
---

## Background

I recently started seeing this error message in [VSCode][0]:

![VSCode Error](/images/vscode-shell-environment/vscode-error.png)

Clicking on the `Learn More` button opens [this FAQ page][1], which says VSCode can be started two different ways:

1. From the terminal, via the `code` command:

```bash
code
```

2. From the user interface, via the app icon:

![Launch VSCode from App Icon](/images/vscode-shell-environment/vscode-app-icon.png 'Test title')

When VSCode is launched via the app icon, it has to do some extra stuff to make sure environment variables set via `.bashrc` or `.zshrc` are properly loaded. If that process (which is basically just launching a shell) takes longer than three or ten seconds, you respectively get a warning and/or error on startup.

## Theory

I have noticed, in the past, that the terminal window opens right away, but sometimes takes a few seconds before it is interactive. It seems the system is still loading and something blocks the terminal process for a few seconds. I think VSCode is experiencing a very similar problem, which could explain why it only happens on startup.

I get lost in enough rabbit holes as it is, so I didn't bother to go down this one any further. Regardless of the exact cause, I needed a solution. I could hit the "Don't Show Again" button, but I decided to try to find a better one. I started to investigate how VSCode was being launched with the hopes that I might be able to change it from the app icon method to the terminal method.

## Startup Applications

Startup applications can be viewed by running:

```bash
gnome-session-properties
```

In this application, you can specify commands to run at startup.

![Startup applications dialog](/images/vscode-shell-environment/gnome-session-properties.png)

Editing the VSCode item shows the details, including the command that's actually run.

![Startup applications edit dialog](/images/vscode-shell-environment/gnome-session-properties-edit.png)

The full command is:

```bash
env BAMF_DESKTOP_FILE_HINT=/var/lib/snapd/desktop/applications/code_code.desktop /snap/bin/code --force-user-env --no-sandbox --unity-launch %F
```

The command looks long and complicated, but the `--force-user-env` argument looks pretty suspicious. This is most definitely the "app icon" method.

## Solution

The solution was pretty simple. I changed this to the "terminal" method by deleting the command and replacing it with `code` instead.

To test it, I restarted my machine 🤞. Luckily, that seemed to have fixed the problem. Everything still worked, and the warning and error messages were gone. Yay! 🎉. To Be fair, I don't use any environment variables set via `.bashrc` in debug targets or tasks... so I'm not 100% that it's being loaded. But hey, the error message is gone right?

## Additional Notes

I'm pretty sure I didn't write that command myself, so I spent a few minutes trying to figure out where it came from. It looked like the command that the VSCode app icon would run, but how exactly did it get added to my startup application list? 🤔

Eventually, I found that [Tweaks][2] comes with a startup application section:

![Tweaks startup application list](/images/vscode-shell-environment/tweaks-startup.png)

The "+" button lets you selected an installed application and it automatically creates the appropriate startup application entry for you.

![Tweaks new startup application](/images/vscode-shell-environment/tweaks-startup-add.png)

This must have been how I added startup applications originally. It seems that tweaks extracts the original startup command from the app and uses it to create the startup item.

Well, at least that mystery is solved.

[0]: https://code.visualstudio.com/
[1]: https://code.visualstudio.com/docs/supporting/faq#_resolving-shell-environment-is-slow-error-warning
[2]: https://wiki.gnome.org/Apps/Tweaks
