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
LeShade is a dedicated Linux GUI for installing and managing ReShade, the popular post-processing injector used to enhance games with ambient occlusion, depth of field, and color correction. It simplifies the process by handling ReShade downloads, injecting them into specific game directories, and providing a clean per-game uninstallation tool. Originally a university project, it has since evolved into a full-featured manager—you can find the full backstory in the old README.
Features:
 * Support for common APIs (DX9, DX10, DX11, DX12, OpenGL)
 * Native Direct3D 8.x support
 * Compatible with both Addon and non-addon ReShade builds
 * Full support for official ReShade release versions
 * Clean uninstallation for specific games
 * Access to multiple shader repositories
Why no Vulkan support?
For Vulkan-based games on Linux, we recommend using vkBasalt instead.
ReShade's Vulkan implementation doesn't work through simple .dll injection; it relies on a specific Windows file structure (like C:\ProgramData\ReShade), specialized .json configurations, and registry keys that point to these paths. This chain often fails within Linux environments. Even after testing manual workarounds—such as installing Vulkan runtimes via protontricks or attempting to replace system .dll files—reliable results were not achieved. While users are welcome to experiment or contribute fixes (see issue #16), Vulkan support is not currently a native feature.
Note: This limitation does not affect DXVK, which works perfectly with LeShade.
Usage
If you have experience with mod managers or the standard ReShade wizard, LeShade will feel very intuitive. You can also follow this video guide. The latest AppImage and Flatpak builds are available on the releases page.
AppImage
 * Download LeShade-x86_64.AppImage.
 * Right-click the file → Properties → Permissions → check Allow executing file as program.
 * Launch the application.
Flatpak
cd ~/Downloads
flatpak install ./LeShade-x86_64.flatpak

Arch Linux (AUR)
Install leshade-git for the latest commits or leshade-bin (maintained by @italoghost) for the latest stable release.
paru -S leshade-bin   # or leshade-git
# or
yay -S leshade-bin    # or leshade-git

Gentoo Linux (GURU)
LeShade is available as games-util/leshade via the GURU overlay.
# Follow GURU setup instructions at the link above
emerge --ask games-util/leshade

Fedora (COPR)
sudo dnf copr enable ishidaw/leshade
sudo dnf install leshade

Direct3D 8.0
Games running on D3D 8.0 require specific environment variables in your game launcher. Below are examples for Steam and Heroic:
<div align="center">
<h4>Steam</h4>
<img alt="Steam launch options" src="[https://i.imgur.com/HEq7U4X.png](https://i.imgur.com/HEq7U4X.png)" width="800" />
<h4>Heroic</h4>

<img alt="Heroic Games Launcher" src="[https://i.imgur.com/Ymj68nY.png](https://i.imgur.com/Ymj68nY.png)" width="800" />

</div>
Development
LeShade is built using PySide6 and standard Qt widgets to ensure seamless system theme integration. The choice of Qt was inspired by its successful implementation in projects like PCSX2, Duckstation, and ShadPS4. The project logo was designed in Inkscape. Notably, LeShade was developed entirely without the use of AI.
Builds have been rigorously tested (via AppImage and Flatpak) on Ubuntu 25.10, Ubuntu 24.04.3, Linux Mint 22.2 (via VirtualBox), and natively on CachyOS. Detailed testing notes can be found in PR #9.
Config files
LeShade manages game data through a manager.json file:
| Version | Path |
|---|---|
| AppImage | ~/.config/leshade/manager.json |
| Flatpak | ~/.var/app/io.github.ishidawg.LeShade/config/leshade/manager.json |
This file tracks the name and directory of each game, allowing the manager to populate the uninstallation list and remove ReShade components without leaving orphan files behind.
Contributing
To contribute, clone the repository, implement your changes, and submit a pull request. Bug reports submitted through GitHub Issues are also highly valued.
git add . && git commit -m "Description of changes" && git push origin main

Please use the following format for pull requests:
## Contribution title

**Have you used AI to vibe code?**
Response.
**Have you used AI as a research source?**
Response.
**Have you tested locally?**
Response.

### Fixes:
Summary of the changes or fixes.

Sources
 * d3dcompiler_47.dll (64-bit & 32-bit) — sourced from Windows SDK 10.0.26100.0
 * d3d8to9.dll — sourced from crosire/d3d8to9
 * AppImage — used for packaging and distribution
LeShade Video Guide
This video provides a visual walkthrough of the LeShade interface and the steps required to install ReShade on Linux games.