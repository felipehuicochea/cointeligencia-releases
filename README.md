# Cointeligencia desktop: test builds

This repository only hosts **test installers** for the Cointeligencia desktop app.
Downloads are on the [Releases](../../releases) page.

> [!WARNING]
> **LIVE-TEST builds can place REAL orders with real funds.**
> - The app **starts in dry-run** (simulated orders) on every launch.
> - Real orders begin **only after** you open **Settings → Live trading (live-test build)**, type `LIVE` and confirm.
> - **Back to dry-run** stops live trading immediately.
> - **Restarting the app always goes back to dry-run.**
> - While the build is a live-test build, a red **LIVE-TEST BUILD** chip is shown. The **LIVE / DRY RUN** chip shows the current mode.
> - All safety limits stay active: max position size, leverage caps, confirmations, and the 30-minute resume window.

## Minimum OS

| Platform | Minimum |
|---|---|
| macOS Apple silicon (M1 or newer) | macOS 12.0 Monterey |
| macOS Intel | macOS 12.0 Monterey |
| Windows x64 | Windows 10 |
| Linux x64 | glibc 2.34 or newer: Ubuntu 22.04, Debian 12, Fedora 35, RHEL / Rocky / Alma 9, or newer |

On Linux, check yours with `ldd --version` (first line, e.g. `2.35`). Ubuntu 20.04 and Debian 11 are **not** supported; their glibc is too old.

## Which file to download

| Platform | File |
|---|---|
| macOS Apple silicon | `Cointeligencia-<version>-arm64.dmg` (or `.zip`) |
| macOS Intel | `Cointeligencia-<version>-x64.dmg` (or `.zip`) |
| Windows (installer) | `Cointeligencia-Setup-<version>.exe` |
| Windows (portable, no install) | `Cointeligencia-<version>-portable.exe` |
| Linux x64 (any distro, no install) | `Cointeligencia-<version>-x86_64.AppImage` |
| Linux x64 (Ubuntu, Debian and derivatives) | `Cointeligencia-<version>-amd64.deb` |

Not sure which Mac you have? Open  menu → **About This Mac**. "Chip: Apple M…" means Apple silicon; "Processor: Intel…" means Intel.

## Install

### macOS
1. Open the `.dmg` and drag **Cointeligencia** to **Applications**. With the `.zip`, unzip it and move the app to Applications.
2. Open it as described below. These builds are not notarized by Apple.

### Windows
1. Run `Cointeligencia-Setup-<version>.exe` and follow the installer. Or just run the portable `.exe`.
2. If SmartScreen appears, see below.

### Linux (x64)
Use either format.

**AppImage** (any distribution, nothing to install):

```sh
chmod +x Cointeligencia-<version>-x86_64.AppImage
./Cointeligencia-<version>-x86_64.AppImage
```

AppImages need FUSE 2. If it doesn't start and mentions `libfuse.so.2`, install it:

```sh
sudo apt install libfuse2      # Ubuntu 22.04
sudo apt install libfuse2t64   # Ubuntu 24.04 and newer (the package was renamed)
```

Do **not** install the `fuse` package on Ubuntu 22.04 or newer; it can remove parts of the desktop.
To skip FUSE entirely, start it with `--appimage-extract-and-run`.
On Ubuntu 24.04 and newer, if the app closes immediately with a sandbox error, start it with `--no-sandbox`.

**.deb** (Ubuntu, Debian and derivatives):

```sh
sudo apt install ./Cointeligencia-<version>-amd64.deb
```

Keep the `./` so apt installs the local file and pulls in its dependencies. The app then appears in your
applications menu as **Cointeligencia**. Remove it with `sudo apt remove cointeligencia-desktop`.

## Opening unsigned test builds

These test builds have no Apple Developer ID or Windows code-signing certificate, so the system warns you the first time you open them.

**macOS**, any one of these:
- Right-click (or Control-click) the app → **Open** → **Open**.
- Try to open it once, then go to **System Settings → Privacy & Security** and click **Open Anyway**.
- In Terminal: `xattr -dr com.apple.quarantine /Applications/Cointeligencia.app`

**Windows:** on the "Windows protected your PC" screen, click **More info → Run anyway**.

### Fallback if a Mac still refuses to open it

Use this if the app still won't open, e.g. with *"The operation couldn't be completed. (OSStatus error 99999.)"*. Run in Terminal:

```sh
xattr -cr /Applications/Cointeligencia.app
codesign --force --deep -s - /Applications/Cointeligencia.app
xattr -cr /Applications/Cointeligencia.app
```

Then open the app again. The second command re-applies a local ad-hoc signature.

## Verify the download (SHA256)

Every release includes a `SHA256SUMS.txt`. Compare it with the checksum of your file:

- **macOS:** `shasum -a 256 ~/Downloads/Cointeligencia-*.dmg`
- **Windows (PowerShell):** `Get-FileHash .\Cointeligencia-Setup-*.exe -Algorithm SHA256`
- **Linux:** in the download folder, `sha256sum -c SHA256SUMS.txt --ignore-missing`

The value must match the line for that file in `SHA256SUMS.txt`. If it doesn't, don't open the file; download it again.

## Reporting bugs

Open an issue in this repository: **Issues → New issue**. Please include:
- Your OS and version (e.g. macOS 12.7 Intel, Windows 11 23H2)
- The exact file you installed (name and release)
- Steps to reproduce, what you expected and what happened
- Screenshots, if possible

> [!CAUTION]
> **Never post API keys, secrets, private keys, wallet keys, passwords or login codes** in issues, screenshots or logs. Blur them out before you post.

## License

The binaries are proprietary test builds. See [NOTICE](NOTICE).
