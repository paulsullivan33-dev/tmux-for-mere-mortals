# What Is tmux?

tmux is a **terminal multiplexer**. That sounds fancy; the idea
is simple: it runs your terminal sessions as a background
**server** on the machine, and your visible terminal is just a
**client** looking at it.

Normally, your shell lives and dies with your terminal window.
Close the window (or drop the SSH connection) and every running
program gets killed. With tmux, the programs run inside the
tmux server. Close the window, and the server keeps going.
Reconnect later — from anywhere — and everything is exactly
where you left it.

## The three layers

tmux organizes things in three layers, biggest to smallest:

- **Session** — a whole workspace. One session might be "the
  duel batch," another "fleet maintenance." Sessions are
  independent and can be detached and reattached.
- **Window** — like a tab in a browser. One session holds many
  windows; you look at one at a time.
- **Pane** — a split within a window. One window can show two
  (or more) terminals side by side or stacked.

```
session "duels"
├── window 0 "batch"      ← you see one window at a time
│   ├── pane 0            ← ...split into panes
│   └── pane 1
└── window 1 "logs"
    └── pane 0
```

## tmux vs screen

If you've used GNU `screen`, tmux is the same idea done newer:
both keep sessions alive across disconnects. Differences that
matter:

- tmux splits panes natively and cleanly; screen's splits are
  clumsy.
- tmux has a real scripting interface (`new-session`,
  `send-keys`, `split-window` as commands, not just keys).
- tmux is actively maintained; screen is essentially frozen.

If screen already does your job, keep it. If you're learning
today, learn tmux.

## What tmux is not

- **Not a remote desktop.** It's text terminals only — no GUI
  apps.
- **Not a process manager.** It keeps sessions alive, but if
  the *machine* reboots, sessions are gone. (For surviving
  reboots, you want systemd services — a different tool.)
- **Not SSH.** tmux doesn't connect anywhere; it just holds
  the session on whatever machine it's running on. Pair it
  *with* SSH (see [tmux Over SSH](tmux-and-ssh.md)) and the
  combination is the whole trick.

**Check:** is tmux installed?

```bash
tmux -V
```

```
tmux 3.4
```

Any 3.x is fine for this guide. Install it with your package
manager if it's missing (`apt install tmux`, `dnf install
tmux`, `brew install tmux`).
