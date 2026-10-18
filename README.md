# tmux-config

Shared [tmux](https://github.com/tmux/tmux) configuration and helper scripts used across:
- **[`.dotfiles`](https://github.com/michalgr/.dotfiles)** (macOS host environment, managed via GNU Stow and Git submodule)
- **[`agent-jail`](https://github.com/michalgr/agent-jail)** (containerized Nix environment, managed via Nix Flakes and Home Manager)

## Structure

```text
tmux-config/
├── .stow-local-ignore     # Excludes repo metadata when stowed into ~/.config/tmux
├── README.md
├── tmux.conf              # Main tmux configuration (Monokai Pro theme, popups, vi mode)
└── bin/                   # Executable helpers (added to $PATH via ~/.config/tmux/bin)
    ├── hx-git             # Opens modified, staged, and untracked Git files in Helix
    └── ta                 # Attaches to or switches/creates tmux sessions
```

## Keybindings

**Prefix:** `Ctrl + Space`

| Key | Action |
| :--- | :--- |
| `Prefix + \|` | Split pane horizontally in current working directory |
| `Prefix + -` | Split pane vertically in current working directory |
| `Prefix + c` | New window in current working directory |
| `Prefix + h/j/k/l` | Vi-style pane navigation |
| `Prefix + f` | FZF session manager popup (`90%` x `90%`) with live pane preview (`ta`) |
| `Prefix + Space` | Quick Actions menu (`Helix (Root)`, `Helix (Git Status)`, `Git Diff`, `LazyGit`, `Shell`, etc.) |
| `Prefix + r` | Reload `~/.config/tmux/tmux.conf` |

## Helper Scripts (`bin/`)

Add `$HOME/.config/tmux/bin` to your `PATH` to use the helper scripts directly:

- **`ta [session-name]`**:
  - Without arguments: opens an interactive `fzf` session manager with live pane preview (`Enter` to switch/attach, `Ctrl-N` to create a new session from the typed query, `Ctrl-X` / `Ctrl-D` to kill a session).
  - With a session name: attaches or switches to `<session-name>`, creating it first if needed.
- **`hx-git`**:
  - Opens all modified, staged, and untracked files in Helix (`hx`), falling back to `hx .` if the working tree is clean.
