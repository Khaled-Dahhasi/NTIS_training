## Setting Up OP-TEE on Raspberry Pi 3

### Installation of Ubuntu Virtual Machine
1. Install a virtual machine on your pc using any Linux OS (e.g., Ubuntu) from the GitHub directory named ['Ubuntu 22.04 (64bit)'](https://github.com/your-username/Ubuntu-VM).

### Build Instructions

#### Step 1 - Prerequisites
Ensure the following prerequisites are installed:
```bash
apt install -y \
     adb \
    acpica-tools \
    autoconf \
    automake \
    bc \
    bison \
    build-essential \
    ccache \
    cpio \
    cscope \
    curl \
    device-tree-compiler \
    e2tools \
    expect \
    fastboot \
    flex \
    ftp-upload \
    gdisk \
    git \
    libattr1-dev \
    libcap-ng-dev \
    libfdt-dev \
    libftdi-dev \
    libglib2.0-dev \
    libgmp3-dev \
    libhidapi-dev \
    libmpc-dev \
    libncurses5-dev \
    libpixman-1-dev \
    libslirp-dev \
    libssl-dev \
    libtool \
    libusb-1.0-0-dev \
    make \
    mtools \
    netcat \
    ninja-build \
    python3-cryptography \
    python3-pip \
    python3-pyelftools \
    python3-serial \
    python-is-python3 \
    rsync \
    swig \
    unzip \
    uuid-dev \
    wget \
    xdg-utils \
    xterm \
    xz-utils \
    zlib1g-dev
```

```bash
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo && chmod a+x ~/bin/repo
mkdir /optee
cd /optee
repo init -u https://github.com/OP-TEE/manifest.git -m rpi3.xml && repo sync -j10
# Set your email and name for repo if prompted
cd /optee/build
```

#### Step 4 - Get the Toolchains
Download the toolchains for different targets:
```bash
cd <optee-project>/build
make -j2 toolchains
```

#### Step 5 - Build the Solution
Build the solution by running:
```bash
make -j `nproc`
```

This step might take some time. To speed up subsequent builds, consider enabling ccache (refer to Tips and Tricks).

### Memory Card Preparation and System Boot

#### Partition and Format Memory Card
To partition, format the memory card, and transfer files, execute:
```bash
make img-help
```
Replace `/dev/sdx1` and `/dev/sdx2` with the correct device name(s) for your computer and SD-card.
You can check using 'sudo fdisk -l' or 'lsblk'


#### Raspberry Pi Setup
1. Insert the SD-card into the Raspberry Pi 3.
2. Connect the UART cable and attach it to the UART.
   ```bash
   picocom -b 115200 /dev/ttyUSB0
   ```
   Install picocom if not already installed: `$ sudo apt-get install picocom`.

3. Power up the Raspberry Pi 3; the system will start booting (visible on UART, not HDMI).

### Testing

#### Step 9 - Run xtest
The xtest test suite is deployed during the previous builds. To run xtest, execute:
```bash
xtest
```

If no regressions/issues are found, xtest should end with a message indicating successful completion.

```plaintext
+-----------------------------------------------------
23476 subtests of which 0 failed
67 test cases of which 0 failed
0 test case was skipped
TEE test application done!
```

---
