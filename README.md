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
</div>LeShade is a Linux GUI tool for installing and managing ReShade — a post-processing injector that adds effects like ambient occlusion, depth of field, and color correction to games. It takes care of downloading ReShade, placing it into the correct game directory, and removing it cleanly when needed. It started as a university project and grew from there. The old README has more background.

Features:

Common API support (DX9, DX10, DX11, DX12, OpenGL)

Direct3D 8.x support

Addon and non-addon ReShade versions

ReShade release version support

Per-game uninstall from previous installations

Multiple shader repositories



---

Why no Vulkan support?

For Vulkan games on Linux, use VkBasalt instead.

ReShade with Vulkan doesn’t work by simply dropping a renamed .dll into the game directory — it depends on a global C:\ProgramData\ReShade folder, specific .dll files, .json configs, and registry entries pointing to that location. On Linux, that setup breaks.

Attempts using protontricks, custom WINEPREFIX setups, and installing VulkanRT-X64-1.4.341.0-Installer.exe didn’t produce reliable results. Replacing vulkan-1.dll in System32 may work for experimentation, but it’s not stable enough to support officially. Contributions to improve this are welcome.

Note: This does not affect DXVK, which works fine. More detail in issue #16.


---

Usage

If you’ve used a mod manager or the ReShade installer before, this should feel familiar. There’s also a video guide. Grab the AppImage or Flatpak from the releases page.

AppImage

1. Download LeShade-x86_64.AppImage


2. Right-click → Properties → Permissions → check Allow executing file as program


3. Run it.



Flatpak

cd ~/Downloads
flatpak install ./LeShade-x86_64.flatpak

Arch Linux (AUR)

leshade-git tracks the latest commit. leshade-bin (thanks @italoghost) tracks the latest release.

paru -S leshade-bin   # or leshade-git
# or
yay -S leshade-bin    # or leshade-git

Gentoo Linux (GURU)

Available as games-util/leshade in GURU.

# Add GURU as described at: https://wiki.gentoo.org/wiki/Project:GURU/Information_for_End_Users
emerge --ask games-util/leshade

Fedora (COPR)

sudo dnf copr enable ishidaw/leshade
sudo dnf install leshade

Direct3D 8.0

Games using D3D 8.0 require environment variables set in your launcher. Examples for Steam and Heroic:

<div align="center">
	<h4>Steam</h4>
	<img alt="Steam launch options" src="https://i.imgur.com/HEq7U4X.png" width="800" />
	<h4>Heroic</h4>
	<img alt="Heroic Games Launcher" src="https://i.imgur.com/Ymj68nY.png" width="800" />
</div>
---

Development

LeShade is built with PySide6 and standard Qt widgets, giving it seamless system theme integration. Qt was chosen after seeing how well it works in apps like PCSX2, DuckStation, and ShadPS4. The logo was made in Inkscape. LeShade was written without AI.

Tested builds (AppImage and Flatpak) on Oracle VirtualBox with Ubuntu 25.10, Ubuntu 24.04.3, and Linux Mint 22.2, as well as CachyOS on real hardware. See PR #9 for details.

Config files

LeShade stores game data in manager.json:

Version	Path

AppImage	~/.config/leshade/manager.json
Flatpak	~/.var/app/io.github.ishidawg.LeShade/config/leshade/manager.json


The file stores each game’s name and path, which is used to populate the uninstall list and remove ReShade cleanly.


---

Contributing

Clone the repo, make your changes, and open a pull request. Bug reports via issues also count as contributions.

git add . && git commit -m "My changes" && git push origin main

Pull requests should follow this format:

## Contribution title

**Have you used AI to write code?**
Response.
**Have you used AI as a research source?**
Response.
**Have you tested locally?**
Response.

### Fixes:
Description of what you fixed.

Sources

d3dcompiler_47.dll (64-bit & 32-bit) — Windows SDK 10.0.26100.0

d3d8to9.dll — crosire/d3d8to9

AppImage — used to build one of the packages