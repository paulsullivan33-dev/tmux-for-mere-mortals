# Windows and Panes

Sessions hold **windows** (tabs — one visible at a time).
Windows hold **panes** (splits — all visible at once). Every
key below starts with the prefix: press `Ctrl-b`, release,
then the key.

## Windows

| Keys | Does |
|---|---|
| `Ctrl-b c` | **c**reate a new window |
| `Ctrl-b n` | **n**ext window |
| `Ctrl-b p` | **p**revious window |
| `Ctrl-b 0`–`9` | jump to window by number |
| `Ctrl-b ,` | rename the current window |
| `Ctrl-b &` | kill the current window (asks first) |

**Check:** after `Ctrl-b c`, the status bar at the bottom shows
two windows:

```
[0] 0:bash* 1:bash-
```

The `*` marks the window you're looking at; `-` marks the
last one you looked at.

## Panes

| Keys | Does |
|---|---|
| `Ctrl-b "` | split top/bottom |
| `Ctrl-b %` | split side-by-side |
| `Ctrl-b` + arrow keys | move between panes |
| `Ctrl-b z` | **z**oom: pane fills the window (press again to unzoom) |
| `Ctrl-b x` | kill the current pane (asks first) |

**Check:** after `Ctrl-b %`:

```bash
tmux list-panes -F '#{pane_index} #{pane_width}x#{pane_height}'
```

```
0 100x50
1 99x50
```

Two panes, side by side.

Mnemonic for the splits: `"` is a horizontal *line*, and it
splits with a horizontal line (top/bottom). `%` has two blobs
side by side, and it splits side by side. It feels backwards
for about a day, then it's automatic.

## Layouts

tmux can rearrange your panes for you:

| Keys | Does |
|---|---|
| `Ctrl-b Space` | cycle through the five layouts |

The layouts are: even-horizontal, even-vertical, main-horizontal,
main-vertical, tiled. Just tap `Space` until it looks right.

## When to use which

- **Windows** for separate *tasks*: one window running the duel
  batch, another tailing logs, a third for general shell work.
- **Panes** for things you watch *together*: logs in one pane,
  `htop` in another, a shell in a third.

Rule of thumb: if you'd tile the terminal windows on your
screen, use panes. If you'd switch tabs, use windows.
