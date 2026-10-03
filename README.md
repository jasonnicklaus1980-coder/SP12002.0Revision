# SP12002.0Revision
SP1200 Inspired MPC Plugin Standalone

## Install
Download `SP1200-2.0.0-mpc-armv7.zip` (in this repository, or from the latest Release), then from a shell on the
MPC (SSH, as root):

    cd /tmp && unzip -o SP1200-2.0.0-mpc-armv7.zip && sh SP1200-2.0.0/install.sh

Full instructions: [SP1200-MPC/mpc/INSTALL.md](SP1200-MPC/mpc/INSTALL.md). Unofficial: Akai has no third-party plugin SDK
for MPC Standalone, so this installs a VST2 plugin registered in MPC.settings (root access; first-generation MPCs).

## Source
| Path | What it is |
|---|---|
| `SP1200-MPC/src/sp1200.cpp` | the plugin: VST2 entry points, parameters, processing |
| `SP1200-MPC/src/sp/` | the SP-1200 model: 12-bit ADC / DAC, aliasing, pitch, SSM2044 filter, reconstruction filters, noise, hardware variation |
| `SP1200-MPC/test/host_test.cpp` | offline host test |
| `SP1200-MPC/tools/` | MPC screen-skin generator |
| `SP1200-MPC/mpc/` | installer, uninstaller, plugin entry, skin, user guide |

## Build
    cd SP1200-MPC
    make test                                                       # native build + host test
    READELF=arm-linux-gnueabihf-readelf ./scripts/package.sh       # ARM plugin + checks + dist/SP1200-2.0.0-mpc-armv7.zip
Needs `g++`, `g++-arm-linux-gnueabihf`, Python 3 with Pillow and `zip`. GitHub Actions (`.github/workflows/sp1200.yml`)
runs the same steps on every push and publishes the install zip as a Release.
