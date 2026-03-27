<div align="center">
	<img src="https://raw.githubusercontent.com/Ishidawg/LeShade/refs/heads/rebuild/assets/logo256.png">
	<h1>LeShade - A Reshade Manager</h1>
	<div display="flex">
		<img alt="GitHub License" src="https://img.shields.io/github/license/ishidawg/LeShade">
		<img alt="GitHub Downloads (all assets, all releases)" src="https://img.shields.io/github/downloads/ishidawg/LeShade/total">
		<img alt="GitHub Repo stars" src="https://img.shields.io/github/stars/ishidawg/LeShade">
	</div>
	<div>
		<a href="https://copr.fedorainfracloud.org/coprs/ishidaw/leshade/package/leshade/"><img src="https://copr.fedorainfracloud.org/coprs/ishidaw/leshade/package/leshade/status_image/last_build.png" /></a>
		<img alt="AUR Version" src="https://img.shields.io/aur/version/leshade-git">
	</div>
</div>

*This started as a university project (mentioned in the [old readme](https://github.com/Ishidawg/LeShade/blob/main/OLD-README.md)), grew into a passion project, and here we are.*

LeShade is a ReShade manager for Linux — think mod manager, but built specifically for ReShade. Features include:

- Common API support *(DX9, DX10, DX11, DX12, OpenGL)*
- Direct3D 8.x support
- Addon and non-addon ReShade versions
- Release version selection
- Per-game uninstall from previous installations
- Multiple shader repositories

### Why no Vulkan support?

For Vulkan games on Linux, [VkBasalt](https://github.com/DadSchoorse/vkBasalt) is the better tool. ReShade's Vulkan support works differently from other APIs — instead of a renamed `.dll` dropped into the game folder, it relies on a global directory (`C:\ProgramData\ReShade`) and registry keys pointing to it. That setup doesn't translate cleanly to Linux. I tried the manual steps and even ran `VulkanRT-X64-1.4.341.0-Installer.exe` through protontricks and WINEPREFIX — no luck. Feel free to try replacing `vulkan-1.dll` in System32 with the runtime from Vulkan's site; maybe you'll have better results. If you know how to fix this properly, contributions are very welcome. See [issue #16](https://github.com/Ishidawg/LeShade/issues/16) for more context.

Note: DXVK is fine — this only applies to **native** Vulkan.

## Usage

The UI is straightforward — if you've used a mod manager or the ReShade installer wizard before, you'll be right at home. There's also a [video guide](https://youtu.be/ge8558huYfE) if you'd prefer that. Download the AppImage or Flatpak from the [releases page](https://github.com/Ishidawg/LeShade/releases).

**AppImage:**
1. Select `LeShade-x86_64.AppImage`
2. Right-click → Properties → Permissions → **Allow executing file as program**
3. Done

**Flatpak:**
1. `cd ~/Downloads`
2. `flatpak install ./LeShade-x86_64.flatpak`
3. Done

### Arch Linux

Two AUR options: `leshade-git` (always latest commit) and `leshade-bin` *(thanks to [@italoghost](https://github.com/italoghost))* (latest release).

```
paru -S leshade-bin   # or yay -S leshade-bin
paru -S leshade-git   # or yay -S leshade-git
```

### Fedora

```
sudo dnf copr enable ishidaw/leshade
sudo dnf install leshade
```

### Direct3D 8.0

Games using Direct3D 8.0 require environment variables set in your launcher (Steam, Heroic, Lutris, Faugus). Examples:

<div align="center">
	<h3>Steam launch options</h3>
	<img alt="Steam launch options" src="https://i.imgur.com/HEq7U4X.png" width="800" />
</div>
<div align="center">
	<h3>Heroic launch options</h3>
	<img alt="Heroic games launcher" src="https://i.imgur.com/Ymj68nY.png" width="800" />
</div>

## Development

LeShade is built with PySide6 and default Qt widgets, which means it integrates cleanly with your system theme. Qt was the obvious pick — PCSX2, Duckstation, and ShadPS4 all use it and they all look great. The project was written entirely by hand, no AI involved.

Builds (AppImage and Flatpak) have been tested on Oracle VM across Ubuntu 25.10, Ubuntu 24.04.3, and Linux Mint 22.2, plus CachyOS on bare metal. See [PR #9](https://github.com/Ishidawg/LeShade/pull/9) for details. The logo was made in Inkscape.

### Config Files

LeShade stores game data in `manager.json` inside the config directory. This file holds each game's name and install path, used for displaying the uninstall list and cleaning up properly.

The location depends on how you installed it:

- **AppImage:** `~/.config/leshade/manager.json`
- **Flatpak:** `~/.var/app/io.github.ishidawg.LeShade/config/leshade/manager.json`

## Contributing

Clone the repo, make your changes, open a pull request. Issues count too — reporting bugs is a genuine contribution.

**PR template:**
```md
## Contribution title

**Did you use AI to vibe-code this?**
Response.
**Did you use AI as a research source?**
Response.
**Did you test this locally?**
Response.

### Fixes:
Description of what you changed.
```

### Sources
- `d3dcompiler_47.dll` (64-bit & 32-bit) from [Windows SDK 10.0.26100.0](https://learn.microsoft.com/en-us/windows/apps/windows-sdk/downloads)
- `d3d8to9.dll` from [crosire](https://github.com/crosire/d3d8to9?tab=readme-ov-file)
- [AppImage](https://github.com/crosire/d3d8to9?tab=readme-ov-file) tool used for packaging
