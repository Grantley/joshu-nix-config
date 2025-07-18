# AGENTS.md

This document provides essential information for AI agents working with this Nix configuration repository.

## Repository Overview

This is a personal Nix configuration repository that manages:
- NixOS system configurations (WSL and Darwin/macOS)
- Home Manager configurations
- Custom Neovim configuration via a local flake
- Shell environment setup (zsh, starship, tmux)
- Development tools and language servers

## Key Commands

### System Rebuilds
```bash
# NixOS (WSL)
sudo nixos-rebuild boot --flake .#joshu-wsl
sudo nixos-rebuild switch --flake .#joshu-wsl

# macOS (Darwin)
sudo darwin-rebuild boot --flake .#joshu-mac
sudo darwin-rebuild switch --flake .#joshu-mac
```

### Home Manager
```bash
# WSL
home-manager switch --flake .#joshu-wsl

# macOS
home-manager switch --flake .#joshu-mac
```

### Maintenance
```bash
# Update flakes
nix flake update

# Update nvim-flake specifically
cd nvim-flake && nix flake update && cd ..

# Clean up old generations
nix-collect-garbage -d

# Quick home-manager update (from Makefile)
make update
```

### GitHub Access Token (if needed)
```bash
NIX_CONFIG='access-tokens = github.com=TOKEN' nix flake update
```

## Project Structure

### Root Configuration Files
- `flake.nix` - Main flake defining system and home configurations
- `configuration.nix` - NixOS system configuration
- `darwin-configuration.nix` - macOS system configuration  
- `home.nix` - Home Manager configuration
- `theming.nix` - Base16 theming configuration

### Neovim Configuration
- `nvim-flake/` - Custom Neovim flake with extensive plugin management
- `nvim-flake/modules/` - Modular Neovim configuration
  - `basic/` - Basic Neovim settings
  - `coding/` - Completion, snippets, AI assistance
  - `colorscheme/` - Theme management
  - `core/` - Core functionality
  - `editor/` - File management, search, navigation
  - `keys/` - Keybindings and which-key
  - `lsp/` - Language server configurations
  - `treesitter/` - Syntax highlighting
  - `ui/` - Status line, notifications, UI elements
  - `util/` - Utility plugins

### Shell Configuration
- `zshrc` - Zsh configuration
- `tmux.conf` - Tmux configuration
- `starship/tokyonight.toml` - Starship prompt theme
- `ghostty` - Ghostty terminal configuration

## Supported Systems

- **joshu-wsl**: NixOS on WSL (x86_64-linux)
- **joshu-mac**: macOS with nix-darwin (aarch64-darwin)

## Key Features

### Development Environment
- **Languages**: Rust, Go, Python, TypeScript, Haskell, C, Lua, Nix
- **Tools**: kubectl, terraform, awscli2, k9s, gh, ripgrep, fzf
- **Editors**: Custom Neovim with LSP, completion, and extensive plugin ecosystem

### Theming
- Base16 theming system with Nord color scheme
- Consistent theming across terminal, editor, and applications

### Package Management
- Declarative package management via Nix
- Separate system and user-level packages
- Flake-based dependency management

## Common Tasks

### Adding New Packages
1. Edit `home.nix` to add packages to `home.packages`
2. Run `home-manager switch --flake .#<system>`

### Updating Neovim Configuration
1. Edit files in `nvim-flake/modules/`
2. Update `nvim-flake/flake.nix` if adding new plugins
3. Run `home-manager switch --flake .#<system>`

### Adding New LSP Support
1. Add language configuration in `nvim-flake/modules/lsp/`
2. Enable in `nvim-flake/flake.nix` defaults
3. Add language server package to `home.nix` if needed

### Troubleshooting
- Check flake inputs are up to date: `nix flake update`
- Verify system matches configuration: `nixos-rebuild dry-run --flake .#<system>`
- Clean build cache: `nix-collect-garbage -d`

## Important Notes

- The Makefile assumes `joshu` profile but flake defines `joshu-wsl` and `joshu-mac`
- GitHub access token may be required for private repositories
- Neovim configuration is modular and can be selectively enabled/disabled
- Base16 theming requires the schemes input to be available