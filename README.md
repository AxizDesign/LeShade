html
<div align="center">
	<img src="https://raw.githubusercontent.com/Ishidawg/LeShade/refs/heads/rebuild/assets/logo256.png">
	<h1>LeShade — A ReShade Manager</h1>
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

LeShade is a Linux GUI application for installing and managing [ReShade](https://reshade.me/) — a popular post-processing injector that adds effects such as ambient occlusion, depth of field, and color correction to games. It automates the download of ReShade, its injection into a game’s directory, and clean per-game uninstallation. The project originated as a university assignment and has since grown into a fully-featured tool. The [old README](https://github.com/Ishidawg/LeShade/blob/main/OLD-README.md) provides additional background.

**Features:**
- Common API support *(DX9, DX10, DX11, DX12, OpenGL)*
- Direct3D 8.x support
- Addon and non-addon ReShade versions
- ReShade release version support
- Per-game uninstall from previous installations
- Multiple shader repositories

---

### Why no Vulkan support?

For Vulkan games on Linux, [VkBasalt](https://github.com/DadSchoorse/vkBasalt) remains the recommended solution.

ReShade’s Vulkan implementation does not work by simply placing a renamed `.dll` into the game directory. It depends on a global `C:\ProgramData\ReShade` folder, specific `.dll` files, `.json` configuration files, and registry keys. On Linux this setup does not translate directly. Manual installation attempts — including running `VulkanRT-X64-1.4.341.0-Installer.exe` via protontricks in a custom WINEPREFIX — were unsuccessful. Replacing `vulkan-1.dll` in System32 may be worth exploring for experimental purposes, and contributions toward a working solution are welcome. For the time being, Vulkan support cannot be provided. (Note: this is unrelated to DXVK, which continues to function correctly.)

More details are available in [issue #16](https://github.com/Ishidawg/LeShade/issues/16).

---

## Usage

If you have previously used a mod manager or the official ReShade installer wizard, LeShade should feel familiar. A short [video guide](https://youtu.be/ge8558huYfE) is also available. The latest AppImage and Flatpak packages can be found on the [releases page](https://github.com/Ishidawg/LeShade/releases).

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

Games using D3D 8.0 require specific environment variables to be set in the game launcher. Examples for Steam and Heroic are shown below:

<div align="center">
	<h4>Steam</h4>
	<img alt="Steam launch options" src="https://i.imgur.com/HEq7U4X.png" width="800" />
	<h4>Heroic</h4>
	<img alt="Heroic Games Launcher" src="https://i.imgur.com/Ymj68nY.png" width="800" />
</div>

---

## Development

LeShade is built with PySide6 and standard Qt widgets, providing seamless integration with the system theme. Qt was selected for its proven reliability in applications such as PCSX2, Duckstation, and ShadPS4. The logo was created manually in Inkscape. The entire project was written by hand, with no AI assistance at any stage.

Builds (AppImage and Flatpak) are tested on Oracle VirtualBox using Ubuntu 25.10, Ubuntu 24.04.3, and Linux Mint 22.2, as well as natively on CachyOS. See [PR #9](https://github.com/Ishidawg/LeShade/pull/9) for complete testing details.

### Config files

LeShade stores game data in `manager.json`:

| Version | Path |
|---|---|
| AppImage | `~/.config/leshade/manager.json` |
| Flatpak | `~/.var/app/io.github.ishidawg.LeShade/config/leshade/manager.json` |

This file records each game’s name and path, enabling accurate uninstall lists and clean removal of ReShade files.

---

## Contributing

Clone the repository, implement your changes, and submit a pull request. Bug reports are also welcome and count as contributions.

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