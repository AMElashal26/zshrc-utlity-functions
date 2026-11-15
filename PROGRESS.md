# PROGRESS — zsh-utility-functions

Handoff / state-of-the-world doc. Answers **"where are we, and why?"** — for
**"what could we do next?"** see [PROPOSALS.md](PROPOSALS.md) (there is no TODO
file yet). Append a dated Session Log entry at the end of any working session;
update the Snapshot when state changes.

## Snapshot (as of 2026-11-15)

- **Repo:** `~/Developer/zsh-utility-functions`, remote
  `github.com/AMElashal26/zshrc-utlity-functions` (note the typo in the remote
  name), branch `main`, 5 commits.
- **`~/.zshrc` is a symlink** to this repo's `.zshrc` (571 lines, 29 aliases,
  ~20 functions). Editing either path edits the same file.
- **`.zshrc` is not committed yet.** It is untracked, so the symlink gives no
  version history until the first commit. Nothing has been pushed with it.
- **Tracked files:** `.gitignore`, `README.md` (title only),
  `functions/pj/README.md`, `functions/pj/pj-function.txt`.
- **Local overrides:** the last line of `.zshrc` sources `~/.zshrc.local` if it
  exists. That file does not exist yet; `.gitignore` already ignores it.
- **Secrets:** none in plaintext. The GitHub token line reads from the macOS
  Keychain.
- **Known mismatch:** the `pj` in the live `.zshrc` is the old version
  (searches `~/Code` and a non-existent `~/Projects`, 2 levels deep). The
  improved version in `functions/pj/pj-function.txt` is not loaded by anything.
- **Backups in `~`:** `~/.zshrc.pre-symlink` (the real file from just before
  the symlink) plus seven older `~/.zshrc.bak*` files.
- **Untracked scratch files in the repo:** `idea-on-symlink.txt` (Raycast AI
  transcript that led to the symlink decision) and
  `idea-on-symlink-txt-what-s-your-take-modular-stonebraker.md` (copy of the
  approved Claude Code plan).

## Current focus

*Unconfirmed — Claude's read, edit freely:* commit `.zshrc` so the symlink
actually delivers version history, then decide whether `functions/` becomes
the real home of the functions or stays a showcase of copies.

## Decision log

| Date | Decision | Why / source |
|---|---|---|
| 2026-11-14 | Track `.zshrc` in git rather than ignore it; keep secrets and machine-specific settings in an ignored `~/.zshrc.local`. | The repo exists to version shell config; the risk is the contents, not the file. Source: `idea-on-symlink.txt`. |
| 2026-11-14 | Source `~/.zshrc.local` from the last line of `.zshrc`, guarded by `[[ -f ]]`. | Last line so private values override tracked ones; the guard keeps a fresh machine error-free. Source: `idea-on-symlink.txt`. |
| 2026-11-15 | `~/.zshrc` is a symlink to the repo copy (not a manual copy, not a sourcing stub). | Two real files drift, and seven hand-made `.bak` files showed git should be doing that job. A dangling link only yields a bare shell and is a one-command fix. Chosen by Ali in the Claude Code session. |
| 2026-11-15 | Deferred: committing `.zshrc`. | It goes to GitHub and contains hardcoded `/Users/aliahmed` paths; Ali decides when. |
| 2026-11-15 | Ideas live in `PROPOSALS.md`, separate from this file. | This file records what is true and decided; proposals are undecided. Accepted proposals get a row here. |

## Doc map

| Doc | What it holds |
|---|---|
| `PROGRESS.md` | This file: state, decisions, session log. |
| `PROPOSALS.md` | Undecided ideas for the repo, each with a why and a rough size. |
| `README.md` | Title only so far. |
| `functions/pj/README.md` | One-line description of the `pj` fuzzy project jumper. |
| `idea-on-symlink.txt` | Raycast AI transcript: gitignore, `.zshrc.local`, symlink-vs-copy debate. Untracked. |
| `~/.claude/plans/idea-on-symlink-txt-what-s-your-take-modular-stonebraker.md` | Approved plan for the symlink, including rollback. |
| `~/progress-hub` | Cross-project mirror. Not confirmed that `note-sync` picks up this repo's path. |

## How to resume cold

1. Read the Snapshot and the newest Session Log entry.
2. Run `ls -l ~/.zshrc` and confirm it still points at this repo. If it is a
   real file again, a tool replaced the link: diff it against the repo copy,
   then re-link.
3. Run `git status` here to see uncommitted config changes.
4. Pick work from `PROPOSALS.md` or from Current focus.
5. After editing `.zshrc`, check it with `zsh -n ~/.zshrc` and
   `zsh -ic 'echo OK'` before closing your only working terminal.
6. Append a Session Log entry and add a Decision log row for anything decided.

Rollback for the symlink: `rm ~/.zshrc && mv ~/.zshrc.pre-symlink ~/.zshrc`.

## Session log (newest first)

### 2026-11-15
- Improved `pj` in `functions/pj/pj-function.txt`: configurable
  `search_roots`, deeper search, pruning of `.git`/`node_modules`/`.venv`
  (`a8f8aad`, `8fbd5a3`).
- Reviewed `idea-on-symlink.txt` with Claude Code. Decided on the symlink;
  moved the real file to `~/.zshrc.pre-symlink` and linked `~/.zshrc` to the
  repo copy. Verified with `zsh -n` and a fresh interactive shell. The two
  files were byte-identical beforehand.
- Created `PROGRESS.md` and `PROPOSALS.md`. Nothing committed in this part of
  the session.
- Next: commit `.zshrc`; reconcile the two `pj` versions.

### 2026-11-14
- Created the repo (`5ac50c5`), added `.gitignore` and the first `pj` fuzzy
  directory hopper (`b6a2dd2`), added its README (`b271836`).
- Raycast AI session: appended the `~/.zshrc.local` sourcing line to
  `~/.zshrc` (backup `~/.zshrc.bak-20261114-233006`) and copied the file into
  the repo. That session ended recommending copy-over-symlink, which was
  reversed on 2026-11-15.
