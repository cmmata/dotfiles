# My Dotfiles

This repository contains my personal dotfiles, managed by [chezmoi](https://www.chezmoi.io/).

## Prerequisites

Before you can use these dotfiles on a new machine, you need to install the following software:

*   [git](https://git-scm.com/)
*   [chezmoi](https://www.chezmoi.io/install/)
*   [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)

## Quick Start on a New Machine

To install and apply these dotfiles on a new computer, run the following command. This will initialize `chezmoi` with this repository and apply the dotfiles to your home directory.

```bash
chezmoi init --apply github.com/appsinet/dotfiles
```

## How It Works

`chezmoi` manages the files in `~/.local/share/chezmoi` (the source directory) and applies them to your home directory (the destination directory).

*   Templates (files ending in `.tmpl`) are executed to generate the final dotfiles.
*   Scripts in `run_...` files are executed at different points in `chezmoi`'s lifecycle. For example, `run_onchange_before_install-packages.sh.tmpl` is used to install packages when changes are applied.
*   The `.chezmoidata` directory contains data that can be used in templates.

## Making Changes

To make changes to your dotfiles, use `chezmoi`'s commands:

*   **Edit a file:** `chezmoi edit <file>`
    *   Example: `chezmoi edit ~/.gitconfig`
*   **Add a new file:** `chezmoi add <file>`
    *   Example: `chezmoi add ~/.new_config_file`
*   **See what changes will be applied:** `chezmoi diff`
*   **Apply the changes:** `chezmoi apply`

After making changes, commit them to this repository:

```bash
cd $(chezmoi source-path)
git add .
git commit -m "Your descriptive commit message"
git push
```

## Ansible

This setup also uses Ansible for provisioning. The `ansible/playbook.yml.tmpl` file is a template for the Ansible playbook. The playbook is likely run by one of the `chezmoi` scripts.
