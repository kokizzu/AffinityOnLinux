# Zorin OS

The packages below are the system dependencies the Affinity installer needs. Zorin OS uses **WineHQ staging** for the best compatibility.

The steps depend on your Zorin version. Follow the section that matches yours.

## Which Section Applies to You?

- **Zorin 18**: use **Section A** (based on Ubuntu 24.04).
- **Zorin 17 and older**: use **Section B** (based on Ubuntu 22.04).

## Section A: Zorin 18

### Step 1: Add the WineHQ Repository

```bash
sudo mkdir -pm755 /etc/apt/keyrings
wget -O- https://dl.winehq.org/wine-builds/winehq.key | sudo gpg --dearmor -o /etc/apt/keyrings/winehq-archive.key
sudo wget -NP /etc/apt/sources.list.d/ https://dl.winehq.org/wine-builds/ubuntu/dists/noble/winehq-noble.sources
```

### Step 2: Install the Dependencies

```bash
sudo apt update
sudo apt install --install-recommends -y winehq-staging \
  winetricks wget curl p7zip-full tar jq zstd \
  dotnet-sdk-8.0 dotnet-sdk-10.0 \
  python3-pyqt6
```

## Section B: Zorin 17 and Older

### Step 1: Add the WineHQ Repository

```bash
sudo mkdir -pm755 /etc/apt/keyrings
wget -O- https://dl.winehq.org/wine-builds/winehq.key | sudo gpg --dearmor -o /etc/apt/keyrings/winehq-archive.key
sudo wget -NP /etc/apt/sources.list.d/ https://dl.winehq.org/wine-builds/ubuntu/dists/jammy/winehq-jammy.sources
```

### Step 2: Install the Dependencies

```bash
sudo apt update
sudo apt install --install-recommends -y winehq-staging \
  winetricks wget curl p7zip-full tar jq zstd \
  dotnet-sdk-8.0 dotnet-sdk-10.0 \
  python3-pyqt6
```

## Verify the Installation (Both Sections)

```bash
which wine winetricks wget curl tar jq zstd
which 7z unzip
dotnet --list-sdks
```

- The first two commands should print file paths. If a line is empty, that package is missing.
- `dotnet --list-sdks` should list versions `8.x` and `10.x`.

## Troubleshooting

- If the .NET SDK packages are not available, you may need to enable Microsoft's repository first. See https://dotnet.microsoft.com/download
- If the installer still reports a missing dependency, close it and reopen it, then click "One-Click Full Setup" again.
