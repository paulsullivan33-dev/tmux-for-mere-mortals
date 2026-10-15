# Your First Session

Five commands cover 90% of tmux: create a session, detach from
it, list sessions, reattach, and kill one when you're done.

## Create

```bash
tmux new-session -s duels
```

You're now *inside* a tmux session named `duels`. It looks like
a normal terminal — that's the point. Run something:

```bash
sleep 600
```

## Detach

Press `Ctrl-b`, release, then press `d`.

You're back at your regular prompt, and tmux tells you:

```
[detached (from session duels)]
```

The `sleep 600` is still running — inside the tmux server,
safe from anything you do out here.

## List

```bash
tmux list-sessions
```

**Check:**

```
duels: 1 windows (created Wed Oct 14 19:35:38 2026)
```

## Reattach

```bash
tmux attach-session -t duels
```

You're looking at the session again. The `sleep` is still
counting down, exactly where you left it. (`-t` means
"target" — which session you're talking to.)

Short forms you'll see everywhere: `tmux ls` for
`list-sessions`, `tmux attach -t duels` or even
`tmux a -t duels`. They all work.

## Kill

When the work is done, kill the session from outside:

```bash
tmux kill-session -t duels
```

Or from inside: type `exit` in every shell (when the last pane
closes, the session ends), or press `Ctrl-b` then `&` to kill
the window.

**Check:**

```bash
tmux list-sessions
```

```
no server running on /tmp/tmux-1000/default
```

That message just means no sessions exist. Nothing is wrong.

## The one habit that matters

**Name your sessions** (`-s duels`, `-s fleet`, `-s build`).
The default names (`0`, `1`, `2`) are fine for one session
and miserable for five. Names cost nothing and save you from
attaching to the wrong thing at 11 PM.
