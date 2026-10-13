# ActVib

Main project for **ActVib**, an experimental system for vibration control and
analysis. ActVib combines an ESP32-based controller, a custom PCB, a desktop
supervisory application and a set of Python helpers to run laboratory
experiments on monitoring, data acquisition, path modeling and active
vibration control.

This repository ties the system together: the software components are
included as Git submodules, so a single clone gives you a consistent set of
versions.

## Components

| Component | Description | Location |
|---|---|---|
| **ActVibFirmware** | Firmware for the ESP32 controller (Arduino). Handles sensor reading (MPU6050, LSM6DS3), ADCs (ADS1x15), DACs (MCP4725) and runs the real-time control algorithms. | [`ActVibFirmware/`](https://github.com/eduardobatista/ActVibFirmware) |
| **ActVibSoftware** | Desktop supervisory application (Python/Qt) for monitoring, acquisition, path modeling, control and firmware updates. | [`ActVibSoftware/`](https://github.com/eduardobatista/ActVibSoftware) |
| **ActVibModules** | Python helpers for working with data acquired by the system: DSP functions, filters, adaptive algorithms, signal generation and a cantilever beam model, with examples. | [`ActVibModules/`](https://github.com/eduardobatista/ActVibModules) |
| **ActVib Board** | Custom PCB that connects the ESP32 board to DACs, ADCs, sensors, etc. | [OSHW Lab](https://oshwlab.com/dudubatista/ic-controle-ativo-de-vibra-es_copy) |
| **Mechanical structure** | Reference mechanical project for a test rig used in experiments with cantilever and fixed-ended beams. | — |

## Getting Started

### Cloning

Clone the repository together with its submodules:

```bash
git clone --recurse-submodules https://github.com/eduardobatista/ActVib.git
```

If you already cloned it without submodules:

```bash
git submodule update --init
```

### Installing the software

Most users only need the desktop application. Installers for Windows and
instructions for Linux are in the
[ActVibSoftware README](ActVibSoftware/README.md) and on its
[Releases page](https://github.com/eduardobatista/ActVibSoftware/releases).

### Updating the firmware

The firmware can be flashed directly from ActVibSoftware via
**Setup > Firmware Update**. See the
[Firmware Update section](ActVibSoftware/README.md#firmware-update) of the
software README for details.

### Using the analysis modules

ActVibModules is a Python package (`numpy`, `scipy`, `pandas`, `plotly`, ...).
Install it in your environment from the submodule:

```bash
pip install ./ActVibModules
```

Then import its modules as `ActVibModules.<module>`. See
`Examples_Basic.ipynb` and the `Examples_*.py` scripts in the
[ActVibModules](ActVibModules/) directory for usage examples.

## Maintaining the Submodules

Each submodule is pinned to a specific commit. To move all of them to the
latest commit of their tracked branches and record the new references:

```bash
git submodule update --init --remote
git add ActVibFirmware ActVibModules ActVibSoftware
git commit -m "Update submodules"
```

## License

See the license file in each component repository (for example,
[ActVibSoftware/LICENSE](ActVibSoftware/LICENSE)).
