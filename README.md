Here we have yet another script for Git-aware customization of the bash command
prompt.  Unlike all the other scripts, I wrote this one, so it's better.

![](screenshot.png)

Features:

- lets you know if you have mail in `$MAIL`
- shows chroot and [virtualenv](https://virtualenv.pypa.io) prompt prefixes
- automatically truncates the current directory path if it gets too long
- shows the status of the current Git repository (see below)
- thoroughly documented and easily customizable


Requirements
============

* Python 3, version 3.5 or higher
* Git, version 1.7.10 or higher
* bash


Installation & Usage
====================

1. Save [`ps1.py`](ps1.py) to your computer somewhere (I put my copy at
   `~/share/ps1.py`)

2. Add the following line to the end of your `~/.bashrc`:

        PROMPT_COMMAND="$PROMPT_COMMAND"'; PS1="$(/usr/bin/python3 ~/share/ps1.py "${PS1_GIT:-}")"'

    Replace `/usr/bin/python3` with the path to your Python 3 interpreter, and
    replace `~/share/ps1.py` with the location you saved `ps1.py` at as
    appropriate.

3. Open a new shell

4. Enjoy!

5. If the Git integration causes you trouble (either because something breaks
   or just because it's taking too long to run), it can be temporarily disabled
   by running `PS1_GIT=off` in bash.


Git Status Symbols
==================

When inside a Git repository, a number of symbols showing the current `HEAD`
and its status are added to the end of the prompt.  Except for the `@`
separator and the `HEAD` itself, individual symbols are omitted when not
relevant.  From left to right, the symbols are:

- `@` — separator
- `+` (bold light yellow) — Indicates there are stashed changes
- the name of the `HEAD` (light green) — the name of the current branch (if
  any), or the name of the currently checked-out tag (if any), or the short
  form of the current commit hash; turns light blue when the repository is in
  detached `HEAD` state
- `+n` (green) — how many commits `HEAD` is ahead of upstream
- `-n` (red) — how many commits `HEAD` is behind upstream
- `*` — Indicates whether there are any staged or unstaged changes in the
  working tree:
    - Green: There are staged changes
    - Red: There are unstaged changes
    - Bold light yellow: There are both staged and unstaged changes
- `+` (bold red) — Indicates there are untracked files in the working tree
- `[STATE]` (magenta) — Shows what activity Git is currently in the middle of,
  if any:
    - `[BSECT]` — bisecting
    - `[CHYPK]` — cherry-picking
    - `[MERGE]` — merging
    - `[REBAS]` — rebasing
    - `[REVRT]` — reverting
- `!` (bold red) — Indicates there are paths with merge conflicts
