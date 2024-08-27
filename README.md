# Biped Firmware

## Table of Contents

1. [Project Prerequisites](#project-prerequisites)
2. [Setting Up the Project](#setting-up-the-project)
3. [Building the Project](#building-the-project)
4. [Labs](#labs)

## Project Prerequisites

This project depends on the installation of the following system packages:

Ubuntu:

```bash
apt install curl tar unzip cmake make doxygen python3-serial
```

macOS:
```bash
brew install curl tar unzip cmake make doxygen python3-serial
```

Click [here](https://brew.sh/) on how to install Homebrew on macOS.

Note: CS 431 students are required to develop this project on the lab workstations. In the case where all lab workstations are fully occupied outside the normal lab sections, students are allowed to temporarily set up and develop this project on their personal computers. However, this project is not fully designed nor guaranteed to work on environments other than the lab workstations. Support from the TA for personal computer setups will be limited.

## Setting Up the Project

On the lab workstation, create a project directory under your home document directory and navigate to the created project directory as follows:
```bash
mkdir -pv ~/Documents/Projects
cd ~/Documents/Projects
```

Under the created project directory above, clone this project using `git clone <project-url> biped-firmware`.

After cloning the project, navigate to the project root directory as follows:
```bash
cd ~/Documents/Projects/biped-firmware
```

To set up the project, run the setup script as follows:
```bash
./scripts/biped-firmware/setup.bash
```

During the setup process, pay close attention to the output of the setup script and check for any errors.

Doxygen will be your best friend for this project. To generate the Doxygen documentation for the project, run the Doxygen script as follows:
```bash
./scripts/biped-firmware/doxygen.bash
```

The Doxygen script will attempt to open the generated documentation in the default web browser. To access the generated documentation manually, navigate to `docs/doxygen/html` and open the `index.html` file using a web browser. Please remember, whenever in doubt, always search in Doxygen first. Refer to the [Doxygen Manual](https://www.doxygen.nl/manual/index.html) for more details regarding Doxygen.

## Building the Project

First, navigate to the project build directory as follows:
```bash
cd ~/Documents/Projects/biped-firmware/build/biped-firmware
```

To build the project, perform the following:
```bash
make
```

To facilitate the building process, enable parallel make jobs when using `make` as follows:
```bash
make -j$(getconf _NPROCESSORS_ONLN)
```

Note: the command `getconf _NPROCESSORS_ONLN` above obtains the number of logical CPU cores in the system.

To flash or upload the built project to the Biped, connect the USB-C cable, and then flash the firmware as follows:
```bash
make -j1 upload SERIAL_PORT=/dev/ttyUSB0
```

It is not recommended to use the upload command above to build the project. Instead, combine the build and upload commands together as follows:
```bash
make -j$(getconf _NPROCESSORS_ONLN) && make -j1 upload SERIAL_PORT=/dev/ttyUSB0
```

The serial port might differ depending on the environment and the operating system.


