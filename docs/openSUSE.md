# openSUSE

This guide covers **openSUSE Tumbleweed and Leap**.

The packages below are the system dependencies the Affinity installer needs. The installer can install them automatically, but these commands let you install them yourself, or recover if the automatic install fails.

## Before You Begin

- You need a user account with `sudo` privileges (the password you enter when installing software).
- Copy and paste the commands one block at a time, then press Enter.
- If a command asks for confirmation, type `y` and press Enter.

## Step 1: Update Your System (Recommended)

Run this first so your package lists are current:

```bash
sudo zypper refresh
```

## Step 2: Install the Dependencies

```bash
sudo zypper install -y wine winetricks wget curl 7zip tar jq zstd python313-PyQt6
```

What these packages do:

| Package | Purpose |
| --- | --- |
| `wine`, `winetricks` | Run the Windows version of Affinity |
| `wget`, `curl` | Download files during setup |
| `7zip`, `tar`, `zstd` | Extract the Wine archive |
| `jq` | Read configuration files |
| `python313-PyQt6` | The graphical interface of the installer |

## Step 3: Install the .NET SDK Packages

These are installed separately so that an unavailable .NET package cannot block the main dependency installation:

```bash
sudo zypper install -y dotnet-sdk-10.0
sudo zypper install -y dotnet-sdk-8.0
```

## Step 4: Verify the Installation

```bash
which wine winetricks wget curl tar jq zstd
which 7z unzip
dotnet --list-sdks
```

- The first two commands should print file paths. If a line is empty, that package is missing.
- `dotnet --list-sdks` should list versions `8.x` and `10.x`.

## Troubleshooting

- If a .NET SDK package cannot be installed (for example, it is temporarily unavailable in the repositories), do not worry. The installer retries automatically later when a patcher needs it.
- If the installer still reports a missing dependency, close it and reopen it, then click "One-Click Full Setup" again.
