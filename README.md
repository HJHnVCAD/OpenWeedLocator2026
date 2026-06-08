<p align="center">
<img src="https://user-images.githubusercontent.com/51358498/152991504-005a1daa-2900-4f48-8bec-d163d6336ed2.png" width="400">
</p>

# OpenWeedLocator (OWL)

**Open-source, low-cost weed detection for site-specific weed control**

[![Tests](https://github.com/geezacoleman/OpenWeedLocator/actions/workflows/tests.yml/badge.svg)](https://github.com/geezacoleman/OpenWeedLocator/actions/workflows/tests.yml)
[![DOI](https://zenodo.org/badge/399194159.svg)](https://zenodo.org/badge/latestdoi/399194159)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.11+](https://img.shields.io/badge/Python-3.11+-blue.svg)](https://www.python.org/downloads/)

OWL is a camera-based weed detection system based on the Raspberry Pi that uses green-detection algorithms to trigger relay-controlled solenoids for spot spraying. It's built entirely from off-the-shelf components and 3D-printable parts, making precision weed control accessible to anyone.

[**Website**](https://www.openweedlocator.org) | [**Documentation**](https://docs.openweedlocator.org) | [**Community**](https://community.openweedlocator.org) | [**Newsletter**](https://openagtech.beehiiv.com/)


### OWLs in Action

<table>
  <tr>
    <th>2m vehicle OWL</th>
    <th>2m robot-mounted OWL</th>
    <th>Bicycle OWL</th>
  </tr>
  <tr>
    <td align="center">
      <img src="https://user-images.githubusercontent.com/51358498/130522810-bb19e6ca-5019-4de4-83cc-858eca358ef8.jpg" width="250"/>
    </td>
    <td align="center">
      <img src="https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/9cb73514-dffc-4c53-969e-c1c816610f1b" width="250"/>
    </td>
    <td align="center">
      <img src="https://github.com/geezacoleman/OpenWeedLocator/assets/51358498/17ad4ead-429e-4384-9e74-b050a536897f" width="250"/>
    </td>
  </tr>

  <tr>
    <th>12m X-fold OWL (in development)</th>
    <th>4m OWL sprayer</th>
    <th>16 channel vegetables OWL</th>
  </tr>
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/c39308cf-ccd7-4428-a10f-fef2fa0ae5af" width="250"/>
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/f32c307d-7fa4-4907-82f2-53519e2236b8" width="250"/>
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/b8c8027a-bacd-41e3-9595-8786ff16b715" width="250"/>
    </td>
  </tr>
</table>

---

## Quick Start

**INSTALL COMPUTE MODULE 5:**

1/ Installed Rpiboot:and used with administrator 
    - on windows : https://github.com/raspberrypi/usbboot/raw/master/win32/rpiboot_setup.exe

2/ Enter Writing Mode on IO board Compute 5

Connect BOOT and GND, set the switch to ON, or just connect the USB-C port. You can check the product page to understand the location of the BOOT pin, for example
https://github.com/HJHnVCAD/OpenWeedLocator2026/tree/main/docs/900px-CM4_Burn_EMMC_1.png


Connect the Micro USB/Type C interface (SLAVE port) of the carrier board to the host PC, then connect a power adapter to the cattier board.

After connecting, the boards should be recognized as BCMxxx devices on Windows PC.
https://github.com/HJHnVCAD/OpenWeedLocator2026/tree/main/docs/200px-CM4_Burn_EMMC_4.png

Run the rpiboot.exe as administrator (The software in the installation directory of Step 2)
link "C:\Program Files (x86)\Raspberry Pi\rpi-mass-storage-gadget64.bat"
https://github.com/HJHnVCAD/OpenWeedLocator2026/tree/main/docs/CM4_Burn_EMMC_5.png

Then the boards will be recognized as a portable disk, just format and write it with a new image.
https://github.com/HJHnVCAD/OpenWeedLocator2026/tree/main/docs/200px-CM4_Burn_EMMC_6.png


3 / Install DEBIAN Trixie OS (64 bit) on CM5 module (Bookworm or Trixie OS) with Raspberry Imager (C:\Program Files (x86)\Raspberry Pi Imager):
with General parameter:
- name host: owl-1.local
- user : owl
- password : owl
with Services :
- activate SSH with password activation for connexion


4/ Restart compute module 5 with screen, keyboard to activate ssh connexion in "Start/Preference/COntrol center" in menu interface 

5/ connected with shh console how "Putty"

6/ If you don't use environnement, before install OpenWeedLocator, install opencv2 for python (opencv-python==4.6.0.66):

```bash
# Clone and install on Raspberry Pi (Bookworm or Trixie OS)
sudo apt-get install libopencv-dev python3-opencv
#or
sudo apt install python3-opencv==4.6.0.66
# or
pip install opencv-python==4.6.0.66
#to control the installation
python3 -c "import cv2; print(cv2.__version__)"
# 4.10.0
```

After, execute this command, with acces public to git repositories:

```bash
# Clone and install on Raspberry Pi (Bookworm or Trixie OS)
git clone https://github.com/HJHnVCAD/OpenWeedLocatorHnVCAD.git owl
bash owl/owl_setup.sh
```

**INSTALL CONTROLLER :Set up the central controller Pi**
```bash
# On the controller Pi (the one with the touchscreen in the cab)
sudo bash owl/controller/networked/in-cab_controller_setup.sh
```
This installs the MQTT broker, the networked dashboard, configures WiFi with a static IP, sets up Nginx, and optionally enables kiosk mode for the touchscreen.

**INSTALL SENSOR OWL : Set up each OWL Pi**
```bash
# On each OWL Pi

sudo bash owl/owl_setup.sh

# When prompted "Do you want to add a web dashboard?" -> yes
# When prompted for mode -> select "Networked"
# Enter the central controller's IP when prompted
```

During this process you'll be asked to setup:
1. Green-on-Green - this adds about 2GB of dependencies
2. Dashboard - standlone or networked

This configures WiFi as a client with a static IP, writes `CONTROLLER.ini` with `mode = networked` and the broker IP pointing to the controller.

**Access:** `https://owl-controller.local/` or `https://<controller-ip>/` (from any device on the same network)

One complete you'll need to reboot and then it should be running.

To confirm, run `sudo systemctl status owl.service` or `sudo journalctl -u owl.service -f`

See the [two step installation guide](https://docs.openweedlocator.org/en/latest/software/index.html) for detailed instructions.

---
---

## Troubleshooting  / Utility ##

This guide covers common issues and solutions for both software and hardware problems with the OWL system.

```{admonition} Report Issues
If you encounter an error that isn't covered here, please [raise an issue on GitHub](https://github.com/HJHnVCAD/OpenWeedLocatorHnVCAD/issues) so we can update this guide and improve the error handling.
```


## Software Errors

The table below includes all current error classes and their hierarchy. All errors include detailed logging, color-formatted terminal output, and standardized error handling. When encountering an error, check the terminal output for specific guidance.

### OWLError

Base exception for all OWL-related errors.

| Error | Common Causes | Solutions |
|-------|---------------|-----------|
| **CameraNotFoundError** | Disconnected camera, damaged ribbon cable, camera not enabled | 1. Check camera connections<br>2. Run `vcgencmd get_camera`<br>3. Enable camera in raspi-config |
| **OWLAlreadyRunningError** | Another OWL instance active, GPIO pins in use | 1. Use `kill <PID>` to stop process<br>2. Check for zombie processes<br>3. Reboot if persists |

### StorageError

Base class for storage-related errors.

| Error | Common Causes | Solutions |
|-------|---------------|-----------|
| **USBMountError** | Device not properly mounted, permission issues | 1. Check physical connection<br>2. Verify mount points<br>3. Check device permissions |
| **USBWriteError** | Write-protected device, full storage, permission issues | 1. Check write protection<br>2. Verify available space<br>3. Check file permissions |
| **NoWritableUSBError** | No USB storage detected, all devices write-protected | 1. Connect USB device<br>2. Check write protection<br>3. Format device if needed |
| **StorageSystemError** | Incompatible platform for storage operation | 1. Use Linux/Raspberry Pi<br>2. Specify a valid local directory in config<br>3. Use `--save-directory` flag |

### OWLControllerError

Base class for controller-related errors.

| Error | Common Causes | Solutions |
|-------|---------------|-----------|
| **ControllerPinError** | Pin conflicts, invalid pin numbers, hardware issues | 1. Check pin configurations<br>2. Verify physical connections<br>3. Check for conflicts |
| **ControllerConfigError** | Missing or invalid configuration | 1. Check config file<br>2. Add missing settings<br>3. Ensure values are appropriate |

### OWLConfigError

Base class for configuration errors.

| Error | Common Causes | Solutions |
|-------|---------------|-----------|
| **ConfigFileError** | Missing config file, invalid file path, corrupt file | 1. Verify file exists<br>2. Check file permissions<br>3. Validate file contents |
| **ConfigSectionError** | Missing required sections in config file | 1. Add missing sections to the config file |
| **ConfigKeyError** | Missing required keys in a section | 1. Add missing keys to the respective config section |
| **ConfigValueError** | Invalid configuration values | 1. Correct values to fit expected ranges |

### Other Errors

| Error | Common Causes | Solutions |
|-------|---------------|-----------|
| **AlgorithmError** | Missing dependencies, invalid model files, Coral device issues | 1. Install required packages<br>2. Verify model files<br>3. Check Coral device connection |
| **OpenCVError** | OpenCV not installed, wrong virtual environment | 1. Run `workon owl`<br>2. Install opencv-python<br>3. Run owl_setup.sh |
| **DependencyError** | Missing Python packages, wrong virtual environment | 1. Activate owl environment<br>2. Run pip install for package<br>3. Install from requirements.txt |

---

## Hardware Issues

Common symptoms and explanations for hardware-related errors.

```{admonition} Update Your Software
:class: warning

If you are using the original disk image without updating, there may be issues that have been fixed. We recommend updating to the latest software using `bash ~/owl/owl_update.sh`.
```

| Symptom | Explanation | Solution |
|---------|-------------|----------|
| **Pi won't start (no green/red lights)** | No power getting to the computer | Check the power source and all downstream components: Bulgin panel/plug connections, fuse connections and fuse, connections to Wago 2-way block, voltage regulator connections, cable into the Raspberry Pi |
| **Pi starts (green light flashing) but no beep** | OWL software has not started | This is likely a configuration/camera connection error. Boot the Pi with a screen connected, open a Terminal (Ctrl + T) and run `~/owl/./owl.py` to see any errors |
| **Beep heard, but no relays activating** | Relays not receiving 12V power, or signal from Pi, or Pi not sending signal | Check all connections with a multimeter for 12V presence. Verify wiring matches the diagram. If connections are correct, run `~/owl/./owl.py` in Terminal to check for errors |

---

## Diagnostic Commands

### Check Camera

```bash
# Check camera is detected
vcgencmd get_camera

# Test camera capture (libcamera)
libcamera-still -o test.jpg
```

### Check OWL Process

```bash
# Check if OWL is running
ps -C owl.py

# Kill existing OWL process
sudo kill <PID>

# View OWL logs
journalctl -u owl -f
```

### Check Virtual Environment

```bash
# Activate OWL environment
workon owl

# Verify packages
pip list | grep opencv
python -c "import cv2; print(cv2.__version__)"
```

### Check Services

```bash
# Check OWL service status
systemctl status owl

# Check dashboard service
systemctl status owl-dash

# Check MQTT broker
systemctl status mosquitto
```

### Check GPIO

```bash
# Check GPIO pin states
gpio readall

# Test relay manually (in Python)
python3 -c "from gpiozero import LED; r = LED(13); r.on(); input('Press Enter'); r.off()"
```

---

## Common Fixes

### Restart OWL Service

```bash
sudo systemctl restart owl
```

### Reboot System

```bash
sudo reboot
```

### Reset Configuration

```bash
# Backup current config
cp ~/owl/config/DAY_SENSITIVITY_2.ini ~/owl/config/DAY_SENSITIVITY_2.ini.backup

# Copy default config
cp ~/owl/config/DAY_SENSITIVITY_2.ini.default ~/owl/config/DAY_SENSITIVITY_2.ini
```

### Reinstall Dependencies

```bash
workon owl
pip install -r ~/owl/requirements.txt
```

### Update OWL Software

```bash
bash ~/owl/owl_update.sh
```

## Documentation Original

- [**Getting Started**](https://docs.openweedlocator.org/en/latest/getting-started/index.html) - What you need, how it works
- [**Hardware Assembly**](https://docs.openweedlocator.org/en/latest/hardware/index.html) - Parts list, wiring, 3D printing
- [**Software Setup**](https://docs.openweedlocator.org/en/latest/hardware/index.html) - Installation, configuration, algorithms
- [**Controller Setup**](https://docs.openweedlocator.org/en/latest/controllers/index.html) - Standalone and networked dashboards
- [**Troubleshooting**](https://docs.openweedlocator.org/en/latest/troubleshooting/index.html) - Common issues and fixes

### Contributing

Contributions are welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines, or join the conversation at [community.openweedlocator.org](https://community.openweedlocator.org).

## Citing OWL

OpenWeedLocator was originally published in [Scientific Reports](https://www.nature.com/articles/s41598-021-03858-9). 
```
@article{Coleman2022,
author = {Coleman, Guy and Salter, William and Walsh, Michael},
doi = {10.1038/s41598-021-03858-9},
issn = {2045-2322},
journal = {Scientific Reports},
number = {1},
pages = {170},
title = {{OpenWeedLocator (OWL): an open-source, low-cost device for fallow weed detection}},
url = {https://doi.org/10.1038/s41598-021-03858-9},
volume = {12},
year = {2022}
}

```
The OWL speed testing paper has been published in [Computers and Electronics in Agriculture](https://www.sciencedirect.com/science/article/pii/S0168169923008074). Please
consider citing the published article using the details below.
```
@article{Coleman2023,
author = {Coleman, Guy R.Y. and Macintyre, Angus and Walsh, Michael J. and Salter, William T.},
doi = {10.1016/j.compag.2023.108419},
issn = {0168-1699},
journal = {Computers and Electronics in Agriculture},
pages = {108419},
title = {{Investigating image-based fallow weed detection performance on Raphanus sativus and Avena sativa at speeds up to 30 km h$^{-1}$}},
url = {https://doi.org/10.1016/j.compag.2023.108419},
volume = {215},
year = {2023}
}
```

### License

This project is licensed under the [MIT License](LICENSE).

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=geezacoleman/OpenWeedLocator&type=Timeline)](https://star-history.com/#geezacoleman/OpenWeedLocator&Timeline)


[def]: image.png