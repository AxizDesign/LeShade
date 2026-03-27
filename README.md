html
<div align="center">
	<img src="https://raw.githubusercontent.com/Ishidawg/LeShade/refs/heads/rebuild/assets/logo256.png">
	<h1>LeShade — A GUI ReShade manager for Linux</h1>
	<div>
		<img alt="GitHub License" src="https://img.shields.io/github/license/ishidawg/LeShade">
		<img alt="GitHub Downloads (all assets, all releases)" src="https://img.shields.io/github/downloads/ishidawg/LeShade/total">
		<img alt="GitHub Repo stars" src="https://img.shields.io/github/stars/ishidawg/LeShade">
	</div>
	<div>
		<a href="https://copr.fedorainfracloud.org/coprs/ishidaw/leshade/package/leshade/"><img src="https://copr.fedorainfracloud.org/coprs/ishidaw/leshade/package/leshade/status_image/last_build.png" /></a>
		<img alt="AUR Version" src="https://img.shields.io/aur/version/leshade-git">
	</div>
</div>

LeShade is a Linux GUI tool for installing and managing [ReShade](https://reshade.me/) — a popular post-processing injector that adds effects such as ambient occlusion, depth of field, and color correction to games. It handles downloading ReShade, injecting it into a game’s directory, and uninstalling everything cleanly on a per-game basis. The project started as a university assignment and has grown from there. The [old README](https://github.com/Ishidawg/LeShade/blob/main/OLD-README.md) provides the full backstory.

**Features:**
- Common API support *(DX9, DX10, DX11, DX12, OpenGL)*
- Direct3D 8.x support
- Addon and non-addon ReShade versions
- ReShade release version support
- Per-game uninstall from previous installations
- Multiple shader repositories

---

### Why no native Vulkan support?

For native Vulkan games on Linux, use [VkBasalt](https://github.com/DadSchoorse/vkBasalt) instead.

ReShade with Vulkan does not work by simply dropping a renamed `.dll` into the game directory. It relies on a global `C:\ProgramData\ReShade` folder, specific `.dll` files, `.json` config files, and registry keys pointing to that location. On Linux that chain does not translate directly. I followed the manual steps and even tried installing `VulkanRT-X64-1.4.341.0-Installer.exe` via protontricks in a custom WINEPREFIX, but it did not work. Replacing `vulkan-1.dll` in System32 is worth trying if you want to experiment, and contributions to fix this are welcome. Vulkan support is not something I can ship right now. (Note: this has no effect on DXVK, which works fine.)

More detail in [issue #16](https://github.com/Ishidawg/LeShade/issues/16).

---

## Usage

If you have used a mod manager or the official ReShade installer wizard before, LeShade should feel familiar. There is also a short [video guide](https://youtu.be/ge8558huYfE). Grab the AppImage or Flatpak from the [releases page](https://github.com/Ishidawg/LeShade/releases).

**AppImage**
1. Download `LeShade-x86_64.AppImage`
2. Right-click → Properties → Permissions → check *Allow executing file as program*
3. Run it.

**Flatpak**
```bash
cd ~/Downloads
flatpak install ./LeShade-x86_64.flatpak
```

**Arch Linux (AUR)**

`leshade-git` tracks the latest commit. `leshade-bin` (thanks [@italoghost](https://github.com/italoghost)) tracks the latest release.
```bash
paru -S leshade-bin   # or leshade-git
# or
yay -S leshade-bin    # or leshade-git
```

**Gentoo Linux (GURU)**

Available as `games-util/leshade` in [GURU](https://wiki.gentoo.org/wiki/Project:GURU).
```bash
# Add GURU as described at: https://wiki.gentoo.org/wiki/Project:GURU/Information_for_End_Users
emerge --ask games-util/leshade
```

**Fedora (COPR)**
```bash
sudo dnf copr enable ishidaw/leshade
sudo dnf install leshade
```

**Direct3D 8.0**

Games using D3D 8.0 require environment variables to be set in your launcher. Examples for Steam and Heroic:

<div align="center">
	<h4>Steam</h4>
	<img alt="Steam launch options" src="https://i.imgur.com/HEq7U4X.png" width="800" />
	<h4>Heroic</h4>
	<img alt="Heroic Games Launcher" src="https://i.imgur.com/Ymj68nY.png" width="800" />
</div>

---

## Development

LeShade is built with PySide6 and standard Qt widgets, which gives it seamless system theme integration. Qt was chosen because it works so well in apps like PCSX2, Duckstation, and ShadPS4. The logo was made in Inkscape. LeShade was written entirely without AI.

Builds (AppImage and Flatpak) are tested on Oracle VirtualBox with Ubuntu 25.10, Ubuntu 24.04.3, and Linux Mint 22.2, plus native runs on CachyOS. See [PR #9](https://github.com/Ishidawg/LeShade/pull/9) for details.

### Config files

LeShade stores game data in `manager.json`:

| Version | Path |
|---|---|
| AppImage | `~/.config/leshade/manager.json` |
| Flatpak | `~/.var/app/io.github.ishidawg.LeShade/config/leshade/manager.json` |

The file stores each game’s name and path — used to populate the uninstall list and to cleanly remove ReShade from a game.

---

## Contributing

Clone the repo, make your changes, and open a pull request. Bug reports via issues count as contributions too.

```bash
git add . && git commit -m "My changes" && git push origin main
```

Pull requests should follow this format:

```md
## Contribution title

**Have you used AI to vibe code?**  
Response.

**Have you used AI as a research source?**  
Response.

**Have you tested locally?**  
Response.

### Fixes:
Description of what you fixed.
```

### Sources
- `d3dcompiler_47.dll` (64-bit & 32-bit) — [Windows SDK 10.0.26100.0](https://learn.microsoft.com/en-us/windows/apps/windows-sdk/downloads)
- `d3d8to9.dll` — [crosire/d3d8to9](https://github.com/crosire/d3d8to9)
- [AppImage](https://appimage.org/) — used to build one of the packages