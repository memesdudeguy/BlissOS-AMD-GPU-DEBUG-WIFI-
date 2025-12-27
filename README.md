# BlissOS(AMD-GPU-DEBUG&WIFI)
# Cloning into 'BlissOS & Tools'...
Username for 'https://github.com': you will need this tools on Ubuntu or any Debain GNU/Linux# 1. Install dependencies (as noted in BlissOS docs)
```
sudo apt update
sudo apt install -y git-core gnupg flex bison gperf build-essential zip curl \
zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses-dev \
x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils \
xsltproc unzip squashfs-tools python3-mako libssl-dev ninja-build lunzip \
syslinux syslinux-utils gettext genisoimage bc xorriso xmlstarlet meson \
glslang-tools git-lfs libncurses6 libncurses6:i386 libelf-dev aapt zstd \
rdfind nasm
```

# Fix libncurses5 compatibility (needed on Ubuntu 24.04+)
```
sudo ln -sf /lib/x86_64-linux-gnu/libncurses.so.6 /lib/x86_64-linux-gnu/libncurses.so.5
sudo ln -sf /lib/x86_64-linux-gnu/libncursesw.so.6 /lib/x86_64-linux-gnu/libncursesw.so.5
sudo ln -sf /lib/x86_64-linux-gnu/libtinfo.so.6 /lib/x86_64-linux-gnu/libtinfo.so.5
sudo ln -sf /lib/i386-linux-gnu/libncurses.so.6 /lib/i386-linux-gnu/libncurses.so.5
sudo ln -sf /lib/i386-linux-gnu/libncursesw.so.6 /lib/i386-linux-gnu/libncursesw.so.5
sudo ln -sf /lib/i386-linux-gnu/libtinfo.so.6 /lib/i386-linux-gnu/libtinfo.so.5
```

# Install Rust toolchain (required)
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source "$HOME/.cargo/env"
cargo install cargo-ndk
rustup target add x86_64-linux-android i686-linux-android
cargo install --version 0.69.1 bindgen-cli
cargo install cbindgen
```
# How to get BlissOS repo
```
nitialize repo with BlissOS manifest (Android 13 = typhoon-x86)
mkdir ~/blissos && cd ~/blissos
repo init -u https://github.com/BlissOS/platform_manifest.git -b typhoon-x86 --git-lfsSync source
repo sync -c --force-sync --no-tags --no-clone-bundle -j$(nproc) --optimized-fetch --prune
```

# For Vanilla (no Google apps)
```
export BLISS_BUILD_VARIANT=vanilla
```
# OR for GApps (MindTheGapps)
```
export BLISS_BUILD_VARIANT=gapps
```
# OR for FOSS (microG + open alternatives)
```
export BLISS_BUILD_VARIANT=foss
```
# If using FOSS, also run:
# ./vendor/foss/update.sh "" bromite  # or just ./vendor/foss/update.sh

# Now to build
```
source build/envsetup.sh
lunch bliss_x86_64-userdebug
make iso_img -j$(nproc)
```
#
