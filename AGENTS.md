# Dotfiles

Managed by **chezmoi** (`chezmoi init --apply appsinet/dotfiles`).  
System packages and fonts installed via **Ansible** (run as a chezmoi `run_onchange_before` hook).

## Supported platforms

- **Fedora Linux** (primary)
- **macOS** (partial — `.zshenv` has a placeholder block)

## Key files

| File | Purpose |
|---|---|
| `.chezmoi.yaml.tmpl` | Prompts for `email` and `username` at init |
| `.chezmoidata/packages.yaml` | Declares `cli` tools and `fonts` for Ansible |
| `dot_zshrc` | Zsh interactive config (Oh My Zsh, plugins, aliases, Starship) |
| `dot_zshenv.tmpl` | Per-platform `$PATH` and env vars |
| `dot_gitconfig.tmpl` | Git identity, aliases, credential helper |
| `ansible/playbook.yml` | Installs dnf packages + Nerd Fonts |
| `run_onchange_before_install-packages.sh.tmpl` | Triggers Ansible when packages/fonts change |

## Conventions

- Source files use chezmoi naming: `dot_` prefix → `.` in home, `.tmpl` suffix for templates.
- Template variables from `.chezmoi.yaml.tmpl` (`.email`, `.username`) or `.chezmoidata/*.yaml`.
- OS-specific logic uses `.chezmoi.osRelease.id` (Linux) and `.chezmoi.os` (darwin).
- Ansible runs locally (`connection: local`, `become: true`) — only for Fedora (RedHat family).
- When adding new CLI tools or fonts, update `.chezmoidata/packages.yaml` only; Ansible picks it up automatically.

## Common tasks

- **Add a cli tool**: add name to `cli` list in `.chezmoidata/packages.yaml`.
- **Add a font**: add name to `fonts` list in `.chezmoidata/packages.yaml`.
- **Add a new dotfile**: `chezmoi add ~/.somefile`, then edit the source in this repo.
- **Apply changes**: `chezmoi apply` (will prompt for sudo password to run Ansible if packages changed).
