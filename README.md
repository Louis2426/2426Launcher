<p align="center">
  <img src="build/2426-launcher-icon.png" alt="2426 Launcher icon" width="112">
</p>

<h1 align="center">2426 Launcher</h1>

<p align="center"><strong>A clean, flexible home for your Minecraft: Java Edition profiles.</strong></p>

<p align="center">
  <a href="./LICENSE"><img src="https://img.shields.io/badge/license-GPLv3-blue.svg" alt="GPL v3 license"></a>
  <a href="https://github.com/beacon-launcher/2426Launcher/releases/latest"><img src="https://img.shields.io/github/v/release/beacon-launcher/2426Launcher?display_name=tag&sort=semver" alt="Latest release"></a>
  <a href="https://github.com/beacon-launcher/2426Launcher/actions/workflows/release.yml"><img src="https://github.com/beacon-launcher/2426Launcher/actions/workflows/release.yml/badge.svg" alt="Build status"></a>
  <a href="https://github.com/beacon-launcher/2426Launcher/releases"><img src="https://img.shields.io/github/downloads/beacon-launcher/2426Launcher/total" alt="Total downloads"></a>
  <img src="https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey" alt="Windows, macOS, and Linux">
</p>

Create separate game profiles, choose a Minecraft version and mod loader, manage mods and
other content, and keep an eye on installs and game logs — all from one desktop app.

> 2426 Launcher does not include Minecraft. Game files are downloaded from Mojang when needed.
> You need a legitimate Minecraft: Java Edition account for online play.

## What you can do

### Profiles and game versions

- Create multiple independent profiles with their own name, icon, Minecraft version, loader,
  memory allocation, installed content, and playtime.
- Choose Vanilla, Fabric, Quilt, Forge, or NeoForge, with available loader versions and
  stable/latest choices where supported.
- Browse releases and snapshots, and change a profile's game version later.
- Automatically install the game files, libraries, assets, natives, and required loader files.
- Repair a profile's installation when files are missing or damaged.
- Install profiles in the background, view progress for multiple installs, or cancel an install.
- Open a profile's game folder directly from the launcher.

### Mods and content

- Browse Modrinth projects and install content for a profile.
- Manage mods, resource packs, data packs, and shaders from the profile page.
- Enable or disable installed items, filter and sort the list, and check for available updates.
- Update items individually or update all items with available updates.
- Drag supported files into the content list to install them.
- Import Modrinth `.mrpack` modpacks from a file, or find and install modpacks from the Home page.
- Review modpack descriptions and project details before installing.
- Check mod compatibility when changing Minecraft versions and warn about detected conflicts
  before launch. Where possible, disable a conflicting mod from the warning.

### Accounts and play

- Add offline usernames for offline/local play.
- Add and switch between multiple accounts from the account menu.
- Use Microsoft sign-in for licensed Minecraft: Java Edition accounts.
- See profile and total playtime.
- View live game output in the built-in console and open persistent launcher logs for troubleshooting.
- Stop a running game from the launcher.

**Microsoft sign-in status:** Minecraft Services currently requires approval of this launcher's
application registration for Java Edition API access. Until that approval is granted, Microsoft
sign-in may stop with an “Invalid app registration” message. This is separate from the
`http://localhost` OAuth redirect setting. See [Microsoft sign-in setup](#microsoft-sign-in).

### Personalization and quality of life

- Choose System, Dark, or Light appearance.
- Select an accent color or create a custom color.
- Use the interface in the available languages.
- Configure global memory and Java paths by Java version; detect an installed Java runtime,
  choose one manually, or install a recommended runtime.
- Enable or disable Discord Rich Presence.
- Resize or collapse the sidebar, navigate with back/forward controls, and use in-app tooltips.
- Check for launcher updates and install supported updates from within the app.

## Roadmap

The ideas below are **planned or under consideration**, not promises or release dates. Priorities
may change based on testing, community feedback, and external API availability.

- **Finish Microsoft sign-in availability:** complete the required Minecraft API app-registration
  approval and verify the full sign-in flow with licensed accounts.
- **Improve profile portability:** explore ways to back up, export, and restore profile settings
  and selected content.
- **Keep improving modpack workflows:** make imports easier to understand and show clearer
  progress and recovery information when a pack fails to install.
- **Polish diagnostics:** continue improving actionable error messages and troubleshooting logs.
- **Ongoing UI and accessibility improvements:** refine navigation, usability, and localization.

Have an idea or found a bug? Open a
[GitHub issue](https://github.com/beacon-launcher/2426Launcher/issues) with steps to reproduce
and, if relevant, the launcher log. Do not include passwords, authorization codes, or tokens.

## Download

Get the latest available build from [GitHub Releases](https://github.com/beacon-launcher/2426Launcher/releases).
Installers are provided for Windows, macOS, and Linux when a release includes those builds.

Builds are currently unsigned, so Windows SmartScreen or macOS Gatekeeper may show a warning
when you first open the app. Only install builds from a source you trust.

## Requirements

- **Java** to run Minecraft. The launcher can detect installed runtimes and offers recommended
  Java installations. As a general guide:
  - Minecraft 1.16 and older: Java 8
  - Minecraft 1.17 through 1.20.4: Java 17 or newer
  - Minecraft 1.20.5 and newer: Java 21 or newer
- **A Microsoft account that owns Minecraft: Java Edition** for licensed online play.
- An internet connection to download game versions, loaders, and Modrinth content.

Set or install Java runtimes in **Settings**. A profile can also use its own memory allocation
instead of the global setting.

## Microsoft sign-in

The launcher uses an OAuth authorization-code flow with PKCE and an embedded Microsoft sign-in
window. The registered redirect URI is exactly:

```text
http://localhost
```

The launcher intercepts the redirect in its login window, so this flow does not run a separate
local callback server. The Microsoft app registration must support personal Microsoft accounts
and public-client authentication.

The redirect URI only configures the Microsoft OAuth handoff. Minecraft Services separately
requires the launcher's app registration to be approved for Java Edition API access. If the
login reports **“Invalid app registration”**, the app needs that approval; changing the redirect,
installing the Xbox app, or adding a local server does not grant it. See the
[Minecraft API app-registration information](https://aka.ms/AppRegInfo) and the
[Minecraft Java Edition third-party application process](https://aka.ms/mce-reviewappid).

## Development

### Prerequisites

- Node.js 18 or newer
- npm
- Git

### Run locally

```bash
git clone https://github.com/beacon-launcher/2426Launcher.git
cd 2426Launcher
npm install
npm run dev
```

### Useful scripts

```bash
npm run typecheck  # check TypeScript types
npm run build      # build main, preload, and renderer into ./out
npm run dev:web    # run the renderer in a browser with a mocked backend
npm run pack       # create an unpacked app in ./dist for a quick smoke test
```

## Build installers

The installer scripts build the app and then package it with
[electron-builder](https://www.electron.build/):

```bash
npm run build:win    # Windows NSIS installer
npm run build:mac    # macOS dmg and zip (x64 and arm64)
npm run build:linux  # Linux AppImage and deb
```

Build output is written to `dist/`. macOS installers must be built on macOS; the release
workflow builds on native runners for each platform.

**Windows note:** local packaging may require symlink permission. Enable Developer Mode in
Windows settings or run the terminal as Administrator. For a quick installer test without
editing/signing the executable:

```bash
npx electron-builder --win --config.win.signAndEditExecutable=false
```

## Releases and updates

The application version is set in `package.json`. Releases are built by
[the release workflow](.github/workflows/release.yml) when a `v*` tag is pushed:

```bash
npm version patch
git push --follow-tags
```

Installed copies check GitHub Releases for updates after startup and on request in
**Settings → Check for updates**. Windows and Linux can download and apply supported updates
in-app. Since macOS builds are unsigned, macOS users may need to download the new build from the
[Releases page](https://github.com/beacon-launcher/2426Launcher/releases).

## Built with

- [Electron](https://www.electronjs.org/) and [React](https://react.dev/)
- [TypeScript](https://www.typescriptlang.org/) and [Vite](https://vite.dev/)
- [`@xmcl`](https://github.com/Voxelum/minecraft-launcher-core-node) for Minecraft installation
  and launch support
- [Modrinth](https://modrinth.com/) for mod and modpack discovery

## License

2426 Launcher is distributed under the
[GPL-3.0-or-later](./LICENSE) license.
