# tmux Over SSH

This is the workflow the whole guide has been building toward:
tmux running on the *remote* machine, SSH just the window you
look through.

## The pattern

```bash
ssh arduino@192.168.1.171
tmux attach -t duels || tmux new-session -s duels
```

That one line is the whole trick: attach if the session
exists, create it if it doesn't. Your Wi-Fi drops? The SSH
process dies, but the tmux server on the box never noticed —
it doesn't care about your connection. Reconnect, run the
same line, and you're exactly where you left off.

## Why this beats nohup

| | `nohup ... &` | tmux |
|---|---|---|
| Survives disconnect | yes | yes |
| See live output later | re-`tail` the log file | attach and *look* |
| Interact with the program | no (it's backgrounded) | yes — it's a real terminal |
| Multiple programs, organized | one background job each | windows and panes, named |
| Restart something | kill, rerun, re-nohup | `Ctrl-c`, up-arrow, Enter |

`nohup` is fine for fire-and-forget. tmux is for work you
come back to.

## A fleet habit

Give every box's long-running job a named session, and make
the names match the job, not the box:

- `duels` on the Q and the Pi — the duel batches
- `fleet` on the Vostro — maintenance shells
- `build` wherever you're compiling

Then "check the duels" is always `tmux attach -t duels`,
whichever box you're on. The name is the interface.

## Nested tmux (SSH inside tmux inside tmux)

Sometimes you run tmux on your laptop *and* on the box you
SSH into. Now `Ctrl-b` goes to the *outer* (laptop) tmux.
To reach the inner one, press the prefix twice: `Ctrl-b`
`Ctrl-b` `d` detaches the *inner* session. (This is what
`bind C-b send-prefix` is for — the default binding already
handles it.)

It works, but it's confusing. Simpler rule: run tmux on the
*remote* box only, and keep your laptop's terminal plain.
One layer of tmux is a tool; two is a puzzle.

## The disconnect test

Don't take any of this on faith — prove it once:

1. SSH into a box, `tmux new-session -s test`, run
   `sleep 300`.
2. Kill your terminal window (don't exit cleanly — yank it).
3. SSH back in, `tmux attach -t test`.

The `sleep` is still running. That feeling — *oh, it just
kept going* — is the entire point of tmux. `tmux kill-session
-t test` when you're done proving it.
