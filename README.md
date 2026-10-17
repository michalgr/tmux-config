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
| `Prefix + f` | FZF session switcher popup with live pane preview |
| `Prefix + Space` | Quick Actions menu (`Helix (Root)`, `Helix (Git Status)`, `Git Diff`, `LazyGit`, `Shell`, etc.) |
| `Prefix + r` | Reload `~/.config/tmux/tmux.conf` |

## Helper Scripts (`bin/`)

Add `$HOME/.config/tmux/bin` to your `PATH` to use the helper scripts directly:

- **`ta [session-name]`**:
  - Without arguments: attaches to the last tmux session (or switches to the previous session if already inside tmux, or creates a new session if none exists).
  - With a session name: attaches or switches to `<session-name>`, creating it first if needed.
- **`hx-git`**:
  - Opens all modified, staged, and untracked files in Helix (`hx`), falling back to `hx .` if the working tree is clean.
