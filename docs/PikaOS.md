# PikaOS

The packages below are the system dependencies the Affinity installer needs. PikaOS uses **WineHQ staging** because its built-in Wine has compatibility issues, and `winetricks` is built from source because the packaged version is not used.

## Before You Begin

- You need a user account with `sudo` privileges (the password you enter when installing software).
- Copy and paste the commands one block at a time, then press Enter.
- If a command asks for confirmation, type `y` and press Enter.
- If you are not sure this is the right path, the [AppImage](../README.md#quick-start) is the supported alternative on PikaOS.

## Step 1: Add the WineHQ Repository

```bash
sudo mkdir -pm755 /etc/apt/keyrings
wget -O- https://dl.winehq.org/wine-builds/winehq.key | sudo gpg --dearmor -o /etc/apt/keyrings/winehq-archive.key
sudo wget -NP /etc/apt/sources.list.d/ https://dl.winehq.org/wine-builds/debian/dists/forky/winehq-forky.sources
```

## Step 2: Install the Dependencies

```bash
sudo apt update
sudo apt install --install-recommends -y winehq-staging \
  wget curl p7zip-full tar jq zstd git \
  python3-pyqt6.qtsvg
```

## Step 3: Install winetricks from Source

```bash
git clone https://github.com/Winetricks/winetricks
cd winetricks
sudo make install
cd ..
rm -rf winetricks
```

## Step 4: Verify the Installation

```bash
which winetricks wget curl tar jq zstd
which 7z unzip
```

- These commands should print file paths. If a line is empty, that package is missing.
- `winetricks` should print a path even though it was built from source.

## Troubleshooting

- If the `make install` step fails, you may be missing build tools. Run `sudo apt install make gcc`, then run Step 3 again.
- If the installer still reports a missing dependency, close it and reopen it, then click "One-Click Full Setup" again.

## Notes

- The GUI installer is not fully supported on PikaOS. If you run into problems, use the [AppImage](../README.md#quick-start) instead.
- The installer installs .NET SDK 8 and 10 automatically later if a patcher needs them. See https://dotnet.microsoft.com/download if those packages are required manually.
