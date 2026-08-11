# Arch Linux

This guide covers **Arch Linux, Artix, CachyOS, EndeavourOS, and XeroLinux**.

The packages below are the system dependencies the Affinity installer needs. The installer can install them automatically, but these commands let you install them yourself, or recover if the automatic install fails.

## Before You Begin

- You need a user account with `sudo` privileges (the password you enter when installing software).
- Copy and paste the commands one block at a time, then press Enter.
- If a command asks for confirmation, type `y` and press Enter.

## Step 1: Update Your System (Recommended)

Run this first so your package lists are current:

```bash
sudo pacman -Syu
```

## Step 2: Install the Dependencies

```bash
sudo pacman -S --needed wine winetricks wget curl p7zip tar jq zstd \
  dotnet-sdk dotnet-sdk-8.0 dotnet-sdk-10.0 \
  python-pyqt6
```

What these packages do:

| Package | Purpose |
| --- | --- |
| `wine`, `winetricks` | Run the Windows version of Affinity |
| `wget`, `curl` | Download files during setup |
| `p7zip`, `tar`, `zstd` | Extract the Wine archive |
| `jq` | Read configuration files |
| `dotnet-sdk-8.0`, `dotnet-sdk-10.0` | Build the patcher the installer uses |
| `python-pyqt6` | The graphical interface of the installer |

## Step 3: Verify the Installation

```bash
which wine winetricks wget curl tar jq zstd
which 7z unzip
dotnet --list-sdks
```

- The first two commands should print file paths. If a line is empty, that package is missing.
- `dotnet --list-sdks` should list versions `8.x` and `10.x`.

## Troubleshooting

- If a package is not found, you skipped Step 1. Run `sudo pacman -Syu`, then run Step 2 again.
- If the installer still reports a missing dependency, close it and reopen it, then click "One-Click Full Setup" again.
- If nothing happens when you double-click the installer, check that `python-pyqt6` is installed (see Step 2).

## Notes

- Manjaro is not officially supported. Use the [AppImage](../README.md#quick-start) instead.
- When the installer installs PyQt6 itself, it adds the `--break-system-packages` flag automatically on these distributions. You do not need to do anything.
