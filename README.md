# ScrollOverview (aarch64 fork)

ScrollOverview is an overview plugin for [Hyprland](https://hypr.land), inspired by niri.

> **This is a fork** of [yayuuu/hyprland-scroll-overview](https://github.com/yayuuu/hyprland-scroll-overview), which is based on the scroll-overview branch of hyprexpo. All credit for the plugin goes to the original author. This fork is maintained for **aarch64** (tested on Asahi Linux, Apple Silicon).

https://github.com/user-attachments/assets/e5eb1ad2-79bc-492a-82cd-02cd8b960d3e

## What's different in this fork

- Removes the dependency on Hyprland function hooks, so the plugin works on aarch64 (tested on Asahi Linux with Arch Linux ARM, Apple Silicon).
- The same changes are available on both the `main` and `new-release` branches.

If you are on x86_64, the [upstream repository](https://github.com/yayuuu/hyprland-scroll-overview) is the reference version.

## Installation

### Using Hyprpm (recommended)

1. Add the plugin repository:
   ```bash
   hyprpm add https://github.com/idrode/hyprland-scroll-overview-aarch4
   ```
   If you use a Git build of Hyprland, add the plugin from the `new-release` branch instead:
   ```bash
   hyprpm add https://github.com/idrode/hyprland-scroll-overview-aarch4 origin/new-release
   ```
2. Build and fetch dependencies:
   ```bash
   hyprpm update
   ```
3. Enable the plugin:
   ```bash
   hyprpm enable scrolloverview
   ```
4. Configure and enjoy.

For more installation methods, including building from source and loading the plugin automatically, see the [upstream Installation guide](https://github.com/yayuuu/hyprland-scroll-overview/wiki/Installation).

## Configuration

### Hyprlang

```ini
# .config/hypr/hyprland.conf
plugin {
    scrolloverview {
        gesture_distance = 300 # how far is the "max" for the gesture
        scale = 0.5 # preferred overview scale
        workspace_gap = 100
        layout = vertical # vertical, horizontal, or auto (per-monitor orientation)
        wallpaper = 2 # 0: global only, 1: per-workspace only, 2: both
        blur = true # blur only the main overview wallpaper

        shadow {
            enabled = true
            range = 50
        }
    }
}

# Toggle ScrollOverview with SUPER+g
bind = SUPER, g, scrolloverview:overview, "toggle all"
```

### Lua

```lua
-- .config/hypr/hyprland.lua
hl.config({
    plugin = {
        scrolloverview = {
            gesture_distance = 300, -- how far is the "max" for the gesture
            scale = 0.5, -- preferred overview scale
            workspace_gap = 100,
            layout = "vertical", -- vertical, horizontal, or auto (per-monitor orientation)
            wallpaper = 2, -- 0: global only, 1: per-workspace only, 2: both
            blur = true, -- blur only the main overview wallpaper

            shadow = {
                enabled = true,
                range = 50,
            },
        },
    },
})

-- Toggle ScrollOverview with SUPER+g
hl.bind("SUPER + g", function()
    hl.plugin.scrolloverview.overview("toggle all")
end)
```

Set `cross_monitor_drag = true` to drag windows between monitors through ScrollOverview and adopt Hyprland move drags when another overview is open. It defaults to `false`. Native adoption uses Hyprland internals; if unavailable, overview-origin cross-monitor dragging still works.

This setting does not affect overview-origin drags with `toggle all` because every overview is already open. Existing multi-monitor commands remain available when it is disabled.

## Documentation

The complete documentation is in the [upstream ScrollOverview wiki](https://github.com/yayuuu/hyprland-scroll-overview/wiki). It covers all configuration options, keybinds, submaps, gestures, dispatchers, and advanced Lua examples.

## Supported plugins

- `hyprbars`

## Credits and license

Original plugin by [yayuuu](https://github.com/yayuuu/hyprland-scroll-overview). This fork keeps the original license; see [LICENSE](LICENSE).
