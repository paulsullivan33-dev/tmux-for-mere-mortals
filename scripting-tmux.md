# Scripting tmux

Everything you can do with keys, you can do from the command
line — and that means you can do it from a **script**. This is
where tmux graduates from "handy" to "infrastructure": whole
workspace layouts launched with one command, no `nohup`
required.

## The core idea

`tmux` commands take a **target** (`-t`) naming the
session/window/pane. So instead of pressing keys inside tmux,
you run:

```bash
tmux new-session -d -s duels            # -d: don't attach, just create
tmux split-window -h -t duels
tmux send-keys -t duels:0.0 'htop' Enter
```

That builds, detached: a session `duels`, split side-by-side,
with `htop` running in the left pane. Attach whenever:

```bash
tmux attach -t duels
```

**Check** (verified on tmux 3.4):

```bash
tmux new-session -d -s verify -x 200 -y 50
tmux split-window -h -t verify
tmux send-keys -t verify:0.0 'echo hello-from-pane-0' Enter
sleep 1
tmux capture-pane -t verify:0.0 -p | grep hello
```

```
hello-from-pane-0
```

`capture-pane -p` prints a pane's contents — handy for checking
on things without attaching.

## A real example: the duel batch

Instead of `nohup python3 ollama_duel.py ... &` and hoping the
SSH session survives, launch it in a named session:

```bash
#!/bin/bash
# start-duels.sh
tmux kill-session -t duels 2>/dev/null   # clean slate if rerun
tmux new-session -d -s duels -n batch \
  'cd ~/dual && python3 ollama_duel.py --profile arduino_q scenarios/'
tmux split-window -h -t duels
tmux send-keys -t duels:0.1 'tail -f ~/dual/runall.log' Enter
```

One command, and you get: the batch running in the left pane,
its log tailing in the right pane, all in a session that
survives your laptop closing. Attach with `tmux attach -t
duels`; detach with `Ctrl-b d`.

## Target syntax

Targets look like `session:window.pane`:

- `duels` — the session (first window, first pane implied)
- `duels:1` — window 1 of session `duels`
- `duels:0.1` — pane 1 of window 0

You can usually abbreviate: if there's only one session,
`-t 0.1` is enough.

## send-keys gotchas

- `send-keys` types *literally* — to "press Enter," pass
  `Enter` as a separate argument (a key *name*, not the
  character).
- Quote the whole command: `send-keys -t s 'cd ~/dual' Enter`
  sends the text, then the key.
- It types into whatever is *currently* in the pane — if a
  program is waiting at a prompt, your keys go there. Make
  sure the pane is at a shell prompt first.

## When scripting beats keys

- **Repeatable setups** — "every morning I open these four
  things" becomes one script.
- **Remote launches** — `ssh box ./start-duels.sh`, close the
  laptop, done. The session outlives the SSH connection.
- **Handoffs** — a script documents the layout; keystrokes
  don't.
