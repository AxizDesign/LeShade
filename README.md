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
LeShade is a handy Linux GUI for installing and managing ReShade—the popular post-processing injector that breathes new life into games with effects like ambient occlusion, depth of field, and custom color correction. Instead of doing everything manually, LeShade takes care of downloading ReShade, safely injecting it right into your game's directory, and easily uninstalling it later on a per-game basis. What started as a simple university project just kept growing. If you're curious about the history, you can read the backstory in the old README.
Features:
 * Common API support (DX9, DX10, DX11, DX12, OpenGL)
 * Direct3D 8.x support
 * Choice between addon and non-addon ReShade builds
 * Support for specific ReShade release versions
 * Clean, per-game uninstallation for previous setups
 * Access to multiple shader repositories
Why no Vulkan support?
If you're playing Vulkan games on Linux, your best bet is to use VkBasalt instead.
Getting ReShade to work with Vulkan isn't as simple as dropping a renamed .dll into a game folder. It actually relies on a global C:\ProgramData\ReShade directory, a mix of specific .dll and .json files, and Windows registry keys that point to them. On Linux, this whole chain just falls apart. I've tried going through the manual setup and even attempted installing VulkanRT-X64-1.4.341.0-Installer.exe using protontricks and setting the WINEPREFIX, but had zero luck. You could try replacing vulkan-1.dll in your prefix's System32 if you really want to experiment, and I'm totally open to contributions if someone figures out a fix! But for now, I just can't ship native Vulkan support.
Just to be clear: this limitation does not affect DXVK, which still works flawlessly. You can find more technical details in issue #16.
Usage
Using LeShade should feel pretty familiar if you've ever messed around with other mod managers or the official Windows ReShade installer wizard. I also put together a quick video guide if you prefer a visual walkthrough. You can grab either the AppImage or Flatpak build over on the releases page.
AppImage
 * Download LeShade-x86_64.AppImage
 * Right-click → Properties → Permissions → check Allow executing file as program
 * Run it.
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
If you're playing older games that use D3D 8.0, you'll need to set up some environment variables directly in your launcher. Here's how that looks in Steam and Heroic:
<div align="center">
<h4>Steam</h4>
<img alt="Steam launch options" src="https://i.imgur.com/HEq7U4X.png" width="800" />
<h4>Heroic</h4>
<img alt="Heroic Games Launcher" src="https://i.imgur.com/Ymj68nY.png" width="800" />
</div>
Development
Under the hood, LeShade is built using PySide6 and standard Qt widgets. I went with Qt because I love how well it integrates with system themes natively, much like what you see in awesome projects like PCSX2, Duckstation, and ShadPS4. The logo itself was crafted in Inkscape, and just as a heads-up, the entire codebase for LeShade was written entirely without the use of AI.
I've tested the AppImage and Flatpak builds inside Oracle VirtualBox running Ubuntu 25.10, Ubuntu 24.04.3, and Linux Mint 22.2, as well as natively on CachyOS outside of a VM. For a deeper dive into the testing specifics, check out PR #9.
Config files
LeShade keeps track of your game data using a manager.json file. Depending on how you installed it, you can find it here:
| Version | Path |
|---|---|
| AppImage | ~/.config/leshade/manager.json |
| Flatpak | ~/.var/app/io.github.ishidawg.LeShade/config/leshade/manager.json |
This file strictly logs the name and directory path of each game you configure. That data is what populates your uninstall list and ensures ReShade is cleanly removed from the right folders when you want to uninstall it.
Contributing
Contributions are always welcome! Feel free to clone the repo, hack away at your changes, and open a pull request. Even if you're just submitting bug reports via the issues tab, that absolutely counts as a contribution.
git add . && git commit -m "My changes" && git push origin main

When you do open a pull request, please make sure it follows this format:
## Contribution title

**Have you used AI to vibe code?**
Response.
**Have you used AI as a research source?**
Response.
**Have you tested locally?**
Response.

### Fixes:
Description of what you fixed.

Sources
 * d3dcompiler_47.dll (64-bit & 32-bit) — Windows SDK 10.0.26100.0
 * d3d8to9.dll — crosire/d3d8to9
 * AppImage — used to build one of the packages