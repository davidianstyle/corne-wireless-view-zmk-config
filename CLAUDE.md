# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a ZMK firmware configuration for a Corne wireless split keyboard with Nice!View displays and a custom dongle setup. The configuration includes:
- Split keyboard halves with Nice!View displays (nice_nano_v2 boards)
- Central dongle with display screen (seeeduino_xiao_ble board)
- Custom keymap with multiple layers

## Key Files and Structure

- `build.yaml` - Defines the build matrix for GitHub Actions (boards, shields, and build configurations)
- `config/west.yml` - West manifest for ZMK and dongle-screen dependencies
- `config/corne.keymap` - Main keymap file with layer definitions
- `config/boards/shields/corne/` - Shield configurations for keyboard and dongle
  - `corne.conf` - Main keyboard configuration
  - `corne_dongle.conf` - Dongle-specific settings with screen configuration
  - `*.overlay` - Device tree overlays for hardware configuration

## Build Commands

The project uses GitHub Actions for automated builds. To trigger a build:
```bash
git push  # Triggers GitHub Actions workflow
```

Firmware artifacts are available from GitHub Actions after successful builds.

## Configuration Notes

### Dongle Configuration
The dongle serves as a central receiver with a display screen showing:
- WPM counter
- Active modifiers
- Current layer
- Output mode (USB/BLE)
- Battery status

Screen controls are mapped to F22-F24 keys in the keymap.

### Bluetooth Profiles
- Supports 5 Bluetooth profiles (configurable via layer 3)
- Central dongle connects to both keyboard halves
- TX power boost enabled for better range

### ZMK Studio
- Enabled on keyboard halves for real-time keymap updates
- Disabled on dongle (display-only device)

## Development Workflow

1. Modify keymap in `config/corne.keymap` or configuration files
2. Push changes to trigger GitHub Actions build
3. Download firmware artifacts from Actions tab
4. Flash firmware files:
   - `corne_left-nice_nano_v2-zmk.uf2` - Left half
   - `corne_right-nice_nano_v2-zmk.uf2` - Right half
   - `corne_dongle-seeeduino_xiao_ble-zmk.uf2` - Dongle
   - `settings_reset-*.uf2` - For clearing settings if needed