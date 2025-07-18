# joshu-nix-config

Personal Nix configuration for NixOS (WSL) and macOS systems with Home Manager integration and custom Neovim setup.

## Features

- **Multi-platform**: Supports both NixOS (WSL) and macOS (Darwin)
- **Custom Neovim**: Comprehensive Neovim configuration with LSP, completion, and 50+ plugins
- **Development Environment**: Pre-configured tools for Rust, Go, Python, TypeScript, Haskell, and more
- **Consistent Theming**: Base16 Nord theme across terminal, editor, and applications
- **Shell Setup**: Zsh with Starship prompt, tmux, and modern CLI tools

## Quick Start

### NixOS (WSL)
```bash
# System configuration
sudo nixos-rebuild switch --flake .#joshu-wsl

# Home Manager configuration
home-manager switch --flake .#joshu-wsl
```

### macOS (Darwin)
```bash
# System configuration
sudo darwin-rebuild switch --flake .#joshu-mac

# Home Manager configuration  
home-manager switch --flake .#joshu-mac
```

## Maintenance

### Update Dependencies
```bash
# Update all flake inputs
nix flake update

# Update nvim-flake specifically
cd nvim-flake && nix flake update && cd ..

# Quick home-manager rebuild
make update
```

### Cleanup
```bash
# Remove old generations
nix-collect-garbage -d
make clean
```

### GitHub Access Token
If you encounter rate limiting during updates:
```bash
NIX_CONFIG='access-tokens = github.com=TOKEN' nix flake update
```

## Structure

- `flake.nix` - Main flake configuration
- `home.nix` - Home Manager packages and settings
- `nvim-flake/` - Custom Neovim configuration flake
- `configuration.nix` - NixOS system configuration
- `darwin-configuration.nix` - macOS system configuration
- `theming.nix` - Base16 theming setup

## Documentation

See [AGENTS.md](./AGENTS.md) for detailed information about the configuration structure and common tasks.
