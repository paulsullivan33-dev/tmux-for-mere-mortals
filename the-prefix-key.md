# The Prefix Key

Every tmux command from the keyboard starts with the **prefix**:
`Ctrl-b`. Press and release it, then press the command key.
`Ctrl-b c` means "hold Ctrl, tap b, release both, tap c."

## Why a prefix at all?

Your terminal already uses most keys — `Ctrl-c` interrupts,
`Ctrl-d` logs out, `Ctrl-z` suspends. tmux needs a namespace
that doesn't collide with anything, so it claims one two-key
sequence (`Ctrl-b` + something) and leaves everything else
alone. Inside tmux, `Ctrl-c` still interrupts your program;
tmux only acts when it sees its prefix first.

## The keys worth memorizing

You don't need all 90+ bindings. This set covers daily life
(verified with `tmux list-keys -T prefix` on tmux 3.4):

**Sessions**

| Keys | Does |
|---|---|
| `Ctrl-b d` | **d**etach (session keeps running) |
| `Ctrl-b s` | list **s**essions, pick one to switch to |

**Windows and panes** — see [Windows and Panes](windows-and-panes.md)
for the full tables. The short list: `c` new window,
`n`/`p` next/previous, `"` and `%` split, arrows move,
`z` zoom, `x` kill pane.

**Everything else**

| Keys | Does |
|---|---|
| `Ctrl-b ?` | list **all** key bindings (searchable help) |
| `Ctrl-b :` | command prompt — type any tmux command by name |
| `Ctrl-b [` | copy mode: scroll back, search, copy text |

`Ctrl-b ?` is the escape hatch: if you forget a key, it's in
there.

## Changing the prefix

`Ctrl-b` is awkward — `b` is typed with the left hand while
Ctrl is also left. Many people switch to `Ctrl-a` (like
`screen` used):

```bash
# ~/.tmux.conf
unbind C-b
set -g prefix C-a
bind C-a send-prefix
```

The third line matters: it lets you send a literal `Ctrl-a`
to the program inside (press `Ctrl-a` twice) — otherwise you'd
have no way to type `Ctrl-a` (start-of-line) in your shell.

**Check:** after reloading (see [Configuring tmux](configuring-tmux.md)):

```bash
tmux show-options -g prefix
```

```
prefix C-a
```

Stick with the default for a week before changing it. Every
tutorial on the internet assumes `Ctrl-b`; learn the standard
first, then customize from a position of knowledge.
