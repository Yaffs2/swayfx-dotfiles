# SwayFX Dotfiles

Distro-agnostic Wayland desktop configuration built around **SwayFX**, styled with a warm **Gruvbox** color palette and **Iosevka Nerd Font**. Originally configured on Gentoo Linux and adaptable to any systemd or OpenRC/runit distribution.

## Components & Aesthetics

* **Compositor:** SwayFX (borderless windows, `5px` inner/outer gaps, `8px` rounded corners, drop shadows, and `200ms` animations)
* **Terminal:** Alacritty (`0.9` opacity, `11.5pt` Iosevka Nerd Font, Gruvbox Material palette)
* **Status Bar:** Waybar (`30px` height with workspace indicators, window title, audio, network, system stats, battery, and tray)
* **App Launcher:** Wofi (Gruvbox dark theme with `#d79921` yellow selection highlights)
* **Font:** `Iosevka Nerd Font`

## Repository Structure

| File | Target Location | Description |
| :--- | :--- | :--- |
| `swayfx-config` | `~/.config/sway/config` | SwayFX keybindings, gaps, rounded corners, shadows, and autostart rules |
| `alacritty.toml` | `~/.config/alacritty/alacritty.toml` | Terminal transparency, font rules, and Gruvbox color scheme |
| `waybar-config.jsonc` | `~/.config/waybar/config.jsonc` | Bar layout and module configurations |
| `waybar-style.css` | `~/.config/waybar/style.css` | Waybar Gruvbox styling and workspace states |
| `wofi-style.css` | `~/.config/wofi/style.css` | Application launcher Gruvbox styling |

## Dependencies

Install the equivalent packages for your distribution:

* **Core Wayland & UI:** `swayfx`, `waybar`, `wofi`, `alacritty`, `swaylock`
* **Screenshots & Screen Recording:** `grim`, `slurp`, `wl-clipboard`, `wf-recorder`
* **Audio, Media & Hardware:** `pipewire` / `pulseaudio` (`pactl`), `pavucontrol`, `playerctl`, `brightnessctl`, `xbacklight`
* **Apps & Fonts:** `thunar`, `iosevka` (Nerd Font patched)

## Installation

1. **Clone the repository:**
   ```bash
   git clone <your-repo-url> ~/sway-dotfiles
   cd ~/sway-dotfiles
   ```

2. **Create configuration directories:**
   ```bash
   mkdir -p ~/.config/{sway,alacritty,waybar,wofi}
   ```

3. **Copy (or symlink) the files to their target paths:**
   ```bash
   cp swayfx-config ~/.config/sway/config
   cp alacritty.toml ~/.config/alacritty/alacritty.toml
   cp waybar-config.jsonc ~/.config/waybar/config.jsonc
   cp waybar-style.css ~/.config/waybar/style.css
   cp wofi-style.css ~/.config/wofi/style.css
   ```

4. **Distro-Specific Adjustments (`~/.config/sway/config`):**
   * **Audio / PipeWire:** Line 165 launches `/usr/bin/gentoo-pipewire-launcher restart`. On non-Gentoo distros, replace or remove this line depending on your init system (e.g., `exec pipewire` on OpenRC/runit, or let `systemd --user` manage PipeWire automatically).
   * **Power Menu (`waybar-config.jsonc`):** The `custom/power` module uses `systemctl suspend` and `systemctl hibernate`. If you use OpenRC, runit, or dinit, update those commands to `loginctl suspend` / `loginctl hibernate` (or `zzz`).
   * **Wallpaper:** Place an image at `~/Pictures/DSCN0145.png` or update the `output * bg` path.

5. **Reload Sway:**
   Press `Super + Shift + C` to reload the configuration.

## Keybindings

Modifier key (`$mod`) is set to **Super** (`Mod4`).

### Applications & System

| Shortcut | Action |
| :--- | :--- |
| `Super + Return` | Open Alacritty terminal |
| `Super + D` | Open Wofi app launcher (`drun`) |
| `Super + E` | Open Thunar file manager |
| `Super + L` | Lock screen (`swaylock`) |
| `Super + Shift + Q` | Kill focused window |
| `Super + Shift + C` | Reload Sway configuration |
| `Super + Shift + E` | Exit Sway session |

### Window & Workspace Management

| Shortcut | Action |
| :--- | :--- |
| `Super + Arrow Keys` | Move focus (`Super + H/K` also mapped for left/up) |
| `Super + Shift + H/J/K/L` | Move focused window (or use `Arrow Keys`) |
| `Super + 1–0` | Switch to workspace 1–10 |
| `Super + Shift + 1–0` | Move focused window to workspace 1–10 |
| `Super + B` / `Super + V` | Split horizontally / vertically |
| `Super + S` / `W` / `Q` | Switch layout: stacking / tabbed / toggle split |
| `Super + F` | Toggle fullscreen |
| `Super + Shift + Space` | Toggle floating mode |
| `Super + Space` | Toggle focus between tiling and floating windows |
| `Super + Shift + -` | Move window to scratchpad |
| `Super + -` | Cycle scratchpad windows |
| `Super + R` | Enter resize mode (`H/J/K/L` or arrows to resize, `Esc`/`Enter` to exit) |

### Screenshots & Screen Recording

| Shortcut | Action |
| :--- | :--- |
| `Print` | Fullscreen screenshot saved to `~/Pictures/` |
| `Super + Shift + S` | Region screenshot saved to `~/Pictures/` (`grim` + `slurp`) |
| `Super + Ctrl + S` | Region screenshot copied to clipboard (`wl-copy`) |
| `Super + Alt + R` | Start screen recording to `~/Videos/` (`wf-recorder`) |
| `Super + Alt + S` | Stop active screen recording |
