# Glossary

**attach** — connect your terminal to a tmux session so you
can see and interact with it. Opposite of *detach*.

**client** — the terminal you're looking at. In tmux's
architecture, the client is disposable: it only displays what
the *server* holds.

**copy mode** — tmux's scrollback viewer (`Ctrl-b [`). Lets
you scroll, search, and copy text from a pane's history.

**detach** — disconnect your terminal from a session without
stopping anything. The session keeps running on the *server*.

**layout** — an arrangement of panes within a window
(even-horizontal, tiled, etc.). Cycle with `Ctrl-b Space`.

**multiplexer** — a program that manages multiple terminal
sessions inside one. tmux and GNU `screen` are the two you'll
meet.

**pane** — one terminal within a window. A window split in
two shows two panes, both live at once.

**prefix** — the key sequence (`Ctrl-b` by default) that tells
tmux "the next key is for you, not the program."

**server** — the background tmux process that owns all
sessions, windows, and panes. It survives closed terminals
and dropped SSH connections. It does *not* survive a reboot.

**session** — a named workspace: a set of windows (and their
panes) you can detach from and reattach to as a unit.

**status bar** — the line at the bottom of a tmux terminal
showing session name, window list, and host/time. Its
presence is the visual proof you're inside tmux.

**target (`-t`)** — which session/window/pane a command acts
on, written `session:window.pane` (e.g. `duels:0.1`).

**window** — like a tab: one session holds many windows, and
you view one at a time. Distinct from a *pane* (splits are
simultaneous; windows are switched between).
