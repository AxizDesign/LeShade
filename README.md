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

LeShade is a Linux GUI tool for installing and managing [ReShade](https://reshade.me/) — the popular post-processing injector that adds effects like ambient occlusion, depth of field, and color correction straight into your games. It takes care of downloading ReShade, injecting it into a game’s folder, and uninstalling everything cleanly on a per-game basis. The whole thing started as a university project and just kept growing from there. The [old README](https://github.com/Ishidawg/LeShade/blob/main/OLD-README.md) has the full backstory if you’re curious.

**Features:**
- Common API support *(DX9, DX10, DX11, DX12, OpenGL)*
- Direct3D 8.x support
- Addon and non-addon ReShade versions
- ReShade release version support
- Per-game uninstall from previous installations
- Multiple shader repositories

---

### Why no Vulkan support?

For Vulkan games on Linux, just use [VkBasalt](https://github.com/DadSchoorse/vkBasalt) instead — it’s the right tool for the job.

ReShade on Vulkan doesn’t work by simply dropping a renamed `.dll` into the game folder. It needs a global `C:\ProgramData\ReShade` folder, specific `.dll` files, `.json` config files, and registry keys that point to everything. On Linux that whole chain falls apart. I tried following the manual steps, even installed `VulkanRT-X64-1.4.341.0-Installer.exe` through protontricks and a custom WINEPREFIX, but it never clicked. Swapping out `vulkan-1.dll` in System32 is something you can experiment with if you want, and I’d love a PR if anyone figures it out. For now, Vulkan support just isn’t something I can ship. (Note: this has nothing to do with DXVK — that works great.)

More details in [issue #16](https://github.com/Ishidawg/LeShade/issues/16).

---

## Usage

If you’ve ever used a mod manager or the official ReShade installer wizard, LeShade will feel right at home. There’s also a short [video guide](https://youtu.be/ge8558huYfE) if you want a quick walkthrough. Grab the AppImage or Flatpak from the [releases page](https://github.com/Ishidawg/LeShade/releases).

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

Games using D3D 8.0 need a couple of environment variables set in your launcher. Here’s how it looks in Steam and Heroic:

<div align="center">
	<h4>Steam</h4>
	<img alt="Steam launch options" src="https://i.imgur.com/HEq7U4X.png" width="800" />
	<h4>Heroic</h4>
	<img alt="Heroic Games Launcher" src="https://i.imgur.com/Ymj68nY.png" width="800" />
</div>

---

## Development

LeShade is built with PySide6 and plain Qt widgets, so it blends perfectly with your system theme. I went with Qt because it just works so well in apps like PCSX2, Duckstation, and ShadPS4. The logo was drawn by hand in Inkscape. And yes — the entire project was written by a human, no AI involved at any point.

I test every build (AppImage and Flatpak) on Oracle VirtualBox with Ubuntu 25.10, Ubuntu 24.04.3, and Linux Mint 22.2, plus native runs on CachyOS. See [PR #9](https://github.com/Ishidawg/LeShade/pull/9) for the full testing details.

### Config files

LeShade keeps track of your games in `manager.json`:

| Version   | Path |
|-----------|------|
| AppImage  | `~/.config/leshade/manager.json` |
| Flatpak   | `~/.var/app/io.github.ishidawg.LeShade/config/leshade/manager.json` |

This file stores each game’s name and path so the uninstall list stays accurate and ReShade can be removed cleanly.

---

## Contributing

Clone the repo, make your changes, and open a pull request. Bug reports count as contributions too — every bit helps.

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