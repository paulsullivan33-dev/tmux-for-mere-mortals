# Troubleshooting

Symptom → fix, in the order you'll hit them.

## "No sessions" right after creating one

**Symptom:** `tmux ls` says `no server running`.

**Cause:** the session's last pane closed (you typed `exit`,
or the command finished), so tmux cleaned up the session.

**Fix:** nothing's broken — that's the design. A session lives
as long as something runs in it. For a persistent session,
leave a shell running in at least one pane.

## Keys do nothing / weird characters appear

**Symptom:** `Ctrl-b` then `c` types `c` instead of opening a
window.

**Cause:** you're not inside tmux (check for the status bar
at the bottom), or your terminal emulator ate the key.

**Fix:** confirm you're attached — the green status bar is
the tell. If keys print odd characters, your `TERM` may be
wrong; `echo $TERM` should say something like
`xterm-256color` or `tmux-256color`, not `dumb`.

## Mouse clicks don't work

**Symptom:** clicking a pane does nothing.

**Cause:** mouse mode defaults to off.

**Fix:** `set -g mouse on` in `~/.tmux.conf`, then
`tmux source-file ~/.tmux.conf`. (Some very old tmux versions
used per-feature mouse options — 2.1+, including the 3.4 used
here, has the single `mouse` switch.)

## "Can't open terminal" / garbled display over SSH

**Symptom:** tmux starts but the screen is garbage, or it
refuses with a terminal error.

**Cause:** the `TERM` your SSH client advertises doesn't
exist on the remote box's terminfo.

**Fix:** inside tmux, run `tmux set -g default-terminal
"screen-256color"` — nearly every box knows that one. Or set
it in `~/.tmux.conf` permanently.

## Session survived, but my program didn't

**Symptom:** reattached to find the program gone, shell
showing "killed" or out-of-memory messages.

**Cause:** tmux protects against *disconnects*, not
*reboots* or the OOM killer. If the box rebooted or ran out
of RAM, the session died with everything else.

**Fix:** for reboot survival you need a service manager
(systemd units, not tmux). For OOM, the program needed less
memory, not a better terminal.

## Nested prefix confusion

**Symptom:** pressing `Ctrl-b d` detaches the wrong session
— you're running tmux inside tmux.

**Cause:** the outer tmux eats the first `Ctrl-b`.

**Fix:** press `Ctrl-b` twice to send one prefix through to
the inner tmux (`Ctrl-b Ctrl-b d` detaches inner). Better:
don't nest — run tmux on the remote box only.

## Copy-paste acts strangely

**Symptom:** selecting text with the mouse copies tmux's
rendering (with line wraps and borders) instead of clean text.

**Cause:** tmux is drawing the terminal; the *terminal
emulator's* selection sees tmux's output, not the program's.

**Fix:** hold **Shift** while selecting — most terminal
emulators bypass the application and select raw screen text.
Or use tmux's copy mode (`Ctrl-b [`) and its own buffers.
