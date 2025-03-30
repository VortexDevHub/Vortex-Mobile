# Development Environment Setup

This guide walks through setting up a development environment for Vortex OS.

## System Requirements

- Linux-based operating system (Ubuntu 22.04 LTS recommended)
- At least 16GB RAM (32GB recommended)
- 500GB+ free disk space
- 64-bit processor with at least 4 cores
- Fast internet connection

## Required Software

- git
- repo tool
- Python 3.8+
- JDK 11
- Rust toolchain (latest stable)
- Android SDK Platform Tools
- LLVM and Clang (latest versions)
- Docker (for isolated build environments)

## Setup Instructions

### 1. Install Base Dependencies

For Ubuntu:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y git-core gnupg flex bison build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z1-dev libgl1-mesa-dev libxml2-utils xsltproc unzip fontconfig
```

### 2. Install Repo Tool

```bash
mkdir -p ~/bin
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
export PATH=~/bin:$PATH
```

### 3. Install Java Development Kit

```bash
sudo apt install -y openjdk-11-jdk
```

### 4. Install Rust Toolchain

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
```

### 5. Install Android SDK Platform Tools

```bash
mkdir -p ~/android/sdk
cd ~/android/sdk
wget https://dl.google.com/android/repository/platform-tools-latest-linux.zip
unzip platform-tools-latest-linux.zip
export PATH=$PATH:~/android/sdk/platform-tools
```

### 6. Configure Git

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### 7. Install Docker

```bash
sudo apt install -y docker.io
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker $USER
```

## Initializing the Build Environment

### 1. Create Working Directory

```bash
mkdir -p ~/vortex-os
cd ~/vortex-os
```

### 2. Initialize Repo

```bash
repo init -u https://github.com/vortex-os/platform_manifest.git -b main
repo sync -j$(nproc --all)
```

### 3. Build Environment Setup

```bash
source build/envsetup.sh
lunch vortex_${device}-userdebug
```

Where `${device}` is the codename of your target device.

### 4. Building Vortex OS

```bash
make -j$(nproc --all)
```

## Troubleshooting

If you encounter issues during setup:

1. Ensure all dependencies are correctly installed
2. Check for system resource limitations
3. Verify network connection for downloading source code
4. Check our GitHub Issues page for known problems

## Getting Help

- Join our Discord server: [link coming soon]
- Check the developer forum: [link coming soon]
- Review documentation at: [docs.vortex-os.org] 