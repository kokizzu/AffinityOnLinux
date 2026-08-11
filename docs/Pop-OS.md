# Pop!_OS

The packages below are the system dependencies the Affinity installer needs. Pop!_OS uses **WineHQ staging** because its built-in Wine has compatibility issues.

## Before You Begin

- You need a user account with `sudo` privileges (the password you enter when installing software).
- Copy and paste the commands one block at a time, then press Enter.
- If a command asks for confirmation, type `y` and press Enter.

## Step 1: Add the WineHQ Repository

```bash
sudo mkdir -pm755 /etc/apt/keyrings
wget -O- https://dl.winehq.org/wine-builds/winehq.key | sudo gpg --dearmor -o /etc/apt/keyrings/winehq-archive.key
sudo wget -NP /etc/apt/sources.list.d/ https://dl.winehq.org/wine-builds/ubuntu/dists/jammy/winehq-jammy.sources
```

## Step 2: Install the Dependencies

```bash
sudo apt update
sudo apt install --install-recommends -y winehq-staging \
  winetricks wget curl p7zip-full tar jq zstd \
  dotnet-sdk-8.0 \
  python3-pyqt6
```

What these packages do:

| Package | Purpose |
| --- | --- |
| `winehq-staging`, `winetricks` | Run the Windows version of Affinity |
| `wget`, `curl` | Download files during setup |
| `p7zip-full`, `tar`, `zstd` | Extract the Wine archive |
| `jq` | Read configuration files |
| `dotnet-sdk-8.0` | Build the patcher the installer uses |
| `python3-pyqt6` | The graphical interface of the installer |

## Step 3: Verify the Installation

```bash
which wine winetricks wget curl tar jq zstd
which 7z unzip
dotnet --list-sdks
```

- The first two commands should print file paths. If a line is empty, that package is missing.
- `dotnet --list-sdks` should list version `8.x` at minimum.

## Troubleshooting

- If the .NET SDK package is not available, you may need to enable Microsoft's repository first. See https://dotnet.microsoft.com/download
- The installer installs .NET SDK 10 automatically later if a patcher needs it. You do not need to install it yourself.
- If the installer still reports a missing dependency, close it and reopen it, then click "One-Click Full Setup" again.
