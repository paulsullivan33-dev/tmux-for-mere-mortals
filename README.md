# tmux for Mere Mortals

**tmux** is a terminal multiplexer: it keeps your terminal
sessions alive on the *server* side, so a dropped SSH connection,
a closed laptop, or a dead Wi-Fi never kills your work. This
guide teaches you to *use* it confidently: sessions, windows,
panes, the prefix key, a sane config file, and scripting it for
real jobs.

No CS degree required. Ideas first, then real commands against
a real tmux.

## What this guide covers

- [**What tmux is**](what-is-tmux.md) — the client/server idea,
  and how it differs from `screen`
- [**Your first session**](your-first-session.md) — create,
  detach, reattach, list, and kill sessions
- [**Windows and panes**](windows-and-panes.md) — splitting
  your screen and organizing work
- [**The prefix key**](the-prefix-key.md) — why `Ctrl-b` exists
  and the keys worth memorizing
- [**Configuring tmux**](configuring-tmux.md) — `~/.tmux.conf`,
  mouse support, and sane defaults
- [**Scripting tmux**](scripting-tmux.md) — launching whole
  layouts from a script (better than `nohup`)
- [**tmux over SSH**](tmux-and-ssh.md) — the fleet workflow:
  sessions that survive disconnects
- [**Troubleshooting**](troubleshooting.md) — symptom → fix,
  seven ways

## What it doesn't cover

Plugins (TPM and the plugin ecosystem), deep copy-mode
customization, and status-bar theming beyond the basics —
this guide is about *using* tmux well, not decorating it.
The [Bash guide](https://paulsullivan33-dev.github.io/bash-for-mere-mortals/)
covers the shell side; the
[SSH guide](https://paulsullivan33-dev.github.io/ssh-for-mere-mortals/)
covers the connection side.

## How to use this guide

Every command was checked against the real tmux 3.4 before
shipping — flags verified, key bindings read from
`tmux list-keys`, config examples loaded with `-f` and confirmed
with `show-options`. **Check:** blocks show verified output.
Anything labeled illustrative says so.

## Chapters

1. [What Is tmux?](what-is-tmux.md)
2. [Your First Session](your-first-session.md)
3. [Windows and Panes](windows-and-panes.md)
4. [The Prefix Key](the-prefix-key.md)
5. [Configuring tmux](configuring-tmux.md)
6. [Scripting tmux](scripting-tmux.md)
7. [tmux Over SSH](tmux-and-ssh.md)
8. [Troubleshooting](troubleshooting.md)
9. [Glossary](glossary.md)
