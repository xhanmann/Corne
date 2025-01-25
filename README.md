# Budget Wireless Corne Keyboard Build

A DIY wireless split keyboard based on the Corne layout, built for approximately $25 USD. This project uses a ProMicro clone with nrf52840 chip, making it a cost-effective alternative to traditional wireless split keyboard builds.

## Features
- Fully wireless using Bluetooth
- Split ergonomic design (Corne layout)
- Low profile design for portability
- Battery-powered with power switch
- ZMK firmware
- Estimated battery life: 1+ month

## Bill of Materials

| Component | Quantity | Cost (USD) | Link |
|-----------|----------|------------|------|
| Controller boards (ProMicro nrf52840) | 2 | 6.82 | [AliExpress](https://a.aliexpress.com/_EIV3vwY) |
| Batteries | 2 | 4.20 | [AliExpress](https://a.aliexpress.com/_Eynt9TK) |
| Mechanical Switches | 50 | 7.47 | [AliExpress](https://a.aliexpress.com/_EGhMxEC) |
| Keycaps | Set | 3.79 | [Option 1](https://a.aliexpress.com/_EzQyNtA) / [Option 2](https://a.aliexpress.com/_EH8mNqs) |
| Diodes (1N4148) | 100 | 0.85 | [AliExpress](https://a.aliexpress.com/_EwZoG2G) |
| Slide Switches | 2 | 0.11 | |
| 3D Printed Parts | Set | 1.80 | Files provided |

**Total Cost**: $25.04 (excluding wires and screws)

## Current Keymap

![image](https://github.com/user-attachments/assets/362ff580-5528-4f7a-ad09-1fa24acbc6c7)
![image](https://github.com/user-attachments/assets/3da97ceb-8e2a-43c5-a241-cf9ad4206688)
![image](https://github.com/user-attachments/assets/cd0f5396-0af1-4aa2-a4e2-1783f79b9708)
![image](https://github.com/user-attachments/assets/2a8999cc-e58c-4d51-a142-067cb7ca768c)
![image](https://github.com/user-attachments/assets/06909fd8-bb4d-4956-88a1-f5d6a8b80e5f)

## Build Instructions

### Prerequisites
- Basic soldering skills
- Access to a 3D printer
- Basic understanding of keyboard firmware

### Case Assembly
1. Print the case files (STL files provided in `3DFiles` directory)
2. Note: You may need to adjust the:
   - Battery compartment size
   - Slide switch holes

### Wiring
1. Wire switches in a matrix configuration
2. Connect diodes:
   - Direction matters (black line indicates cathode)
   - Use diode legs for the rows
   - Use separate wires for columns
3. Keep wiring clear of screw holes
4. Connect the battery:
   - GND to GND pin
   - Positive to one of the side legs on the slide switch
   - Middle pin of the slide switch to the RAW pin

### Pin Connections for Rows and Columns
The matrix configuration uses GPIO pins on the nRF52840 Pro Micro clone. Below are the connections:

![pinout](https://github.com/user-attachments/assets/ae1bf9eb-8071-4a8f-8cac-c95a39f61f9e)

#### Rows (Connected to `row-gpios`):
- Row 0: Pin 21
- Row 1: Pin 20
- Row 2: Pin 19
- Row 3: Pin 18

#### Columns (Connected to `col-gpios`):
- Column 0: Pin 2
- Column 1: Pin 7
- Column 2: Pin 6
- Column 3: Pin 5
- Column 4: Pin 4
- Column 5: Pin 3

These pins are defined in the firmware and are configured for GPIO matrix scanning.

### Firmware Setup
This keyboard uses ZMK firmware. The left half acts as the main controller that connects to your device.

To flash the firmware:
1. Double press the reset button
2. Board will appear as mass storage device
3. Flash the appropriate firmware file

If you forgot the keyboard from your device and can't reconnect:
1. Flash the `settings_reset-nice_nano_v2-zmk.uf2` file
2. Reflash the regular firmware
3. Pair

## Repository Structure
```
├── .github/workflows/
│   └── build.yml
├── 3DFiles/
│   ├── Case_Left.stl
│   ├── Case_Right.stl
│   └── PlateCorne.stl
├── config/
│   ├── boards/shields/corne/
│   │   ├── corne_left.conf
│   │   ├── corne_left.overlay
│   │   ├── corne_right.conf
│   │   ├── corne_right.overlay
│   │   ├── corne.conf
│   │   ├── corne.dtsi
│   │   ├── Kconfig.defconfig
│   │   └── Kconfig.shield
│   ├── corne.keymap
│   └── west.yml
├── firmware/
│   ├── corne_left-nice_nano_v2-zmk.uf2
│   ├── corne_right-nice_nano_v2-zmk.uf2
│   └── settings_reset-nice_nano_v2-zmk.uf2
└── zephyr/
    ├── module.yml
    └── build.yaml
```

## Known Issues
- Left side case may have warping issues if battery swells
- Slide switch holes may need adjustment based on your components
