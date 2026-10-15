# Configuring tmux

tmux reads `~/.tmux.conf` when its server starts. A dozen lines
turn the defaults from "fine" into "yours."

## A sane starting config

```bash
# ~/.tmux.conf

# mouse: click panes, drag to resize, scroll the wheel
set -g mouse on

# keep more scrollback (default is 2000 lines)
set -g history-limit 10000

# windows renumber themselves when one closes (no gaps: 0,1,3)
set -g renumber-windows on

# numbering starts at 1, not 0 (easier to reach)
set -g base-index 1
setw -g pane-base-index 1

# longer to read the status messages (default: 750ms)
set -g display-time 2000

# snappier Escape key (default 500ms delay annoys vim users)
set -s escape-time 10
```

Every line above was loaded with `tmux -f` and confirmed with
`tmux show-options -g` on tmux 3.4.

## Reloading

Config is read when the **server** starts, not when you open a
new terminal. After editing, reload without restarting:

From inside tmux: `Ctrl-b :` then type

```
source-file ~/.tmux.conf
```

Or from your shell:

```bash
tmux source-file ~/.tmux.conf
```

**Check:**

```bash
tmux show-options -g mouse
```

```
mouse on
```

Note: already-running sessions pick up most options, but
`base-index` only affects *new* windows — old ones keep their
numbers until recreated.

## What each setting actually does

- **`mouse on`** — the big one. Click to focus panes, drag
  borders to resize, scroll with the wheel (enters copy mode
  automatically). If you only change one thing, change this.
- **`history-limit`** — lines of scrollback per pane. Logs
  scroll fast; 10000 is cheap (a few MB per pane at most).
- **`renumber-windows`** — kill window 1 of 0,1,2 and the rest
  become 0,1 instead of leaving a gap.
- **`escape-time`** — tmux waits this long after `Escape` to
  see if it's part of an escape sequence. 500ms makes vim feel
  laggy; 10ms is snappy. (Set to 0 and some terminals
  misbehave — 10 is the safe floor.)

## What not to bother with yet

Status-bar theming, plugins (TPM), and copy-mode key
rebinding are all real tmux hobbies — and all skippable until
the basics are muscle memory. A plain status bar that shows
session and window names is enough to work.
