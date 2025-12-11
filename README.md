<h1 align="center">
  <img src="https://github.com/user-attachments/assets/fd00aeb9-993f-41d0-811c-a98a977dc7e1" width="300" height="auto"/>
  <br><br>
  Reflow Hot Plate
  <br><br>
</h1>

<p align="center">
  <a href="#features">Features</a> •
  <a href="#design">Design</a> •
  <a href="#hardware">Hardware</a> •
  <a href="#desktop-application">Desktop Application</a> •
  <a href="#firmware">Firmware</a> •
  <a href="#gallery">Gallery</a> •
  <a href="#usage">Usage</a> •
  <a href="#citation">Citation</a> •
  <a href="#license">License</a>
</p>

The STM32-Based Reflow Hot Plate Project is an open-source initiative aimed at creating a reflow soldering hot plate using the STM32 microcontroller. This project provides an affordable and customizable solution for hobbyists looking to solder surface-mount components onto printed circuit boards with precision and control.

## Features

- IMS PCB heatbed capable of reaching 210°C, with uniform thermal distribution.
- PID-based temperature control with ±5°C accuracy.
- Redundant sensing with PT100 RTD (ADC) and K-type thermocouple (MAX6675 via SPI).
- User interface with OLED (I²C), tactile buttons, and LEDs.
- USB CDC connectivity for desktop control and logging.
- Safety features: watchdog, over-temp detection, error recovery.
- Modular design: heatbed, control board, and front panel separable.

## Design

The device operates with a 24V, 5A external power supply and includes a fuse for protection. A buck converter steps down the voltage, followed by a linear regulator that ensures stability for the analog circuitry.

For temperature measurement, two sensors provide redundancy:
- A PT100 RTD connects to the ADC of the microcontroller.
- A thermocouple (TC) interfaces via SPI using a dedicated IC.

An STM32 microcontroller manages the system due to its extensive documentation, peripheral options, and familiarity. It:
- Controls temperature in a closed loop using PWM to regulate the heating element.
- Handles the user interface, with a screen displaying temperature and status, and buttons for menu navigation and operation.

A USB CDC connection enables communication with a desktop application for remote control and temperature monitoring.

The heating element uses an IMS PCB, allowing customization of size, temperature, and power. It can be replaced if damaged.

The reflow plate includes safety features such as over-temperature, overcurrent, and short-circuit protection for reliability.

The hardware consists of three main parts:
1. Heatbed – Heats the PCB.
1. Control board – Manages heating and user interaction.
1. Front panel – Displays status and allows user input.

<br>
<div align="center">
  <img src="https://github.com/user-attachments/assets/12ac57f4-dc83-411c-b3e9-971c5882201d" width="75%"></img>
  <br><br>
  <em>Block diagram of the project.</em>
</div>
<br>

## Hardware

The electronic hardware is designed using KiCad. It includes the following components:

- STM32 microcontroller (STM32F103 series)
- N-Channel Power MOSFET for controlling the heating element
- Thermocouple and PT100 sensor for temperature measurement
- OLED display for real-time temperature and soldering progress information
- Buttons for user interaction
- USB-C connector for communication
- Power supply circuitry

The mechanical hardware is designed using FreeCAD. It includes the following components:

- Front panel mask
- Front panel brackets
- Gooseneck mounting

These components are designed to be 3D printed and assembled together to create a complete device.

For detailed hardware schematics, PCB layout and CAD models, please refer to the [Hardware](hardware/) directory.

<br>
<div align="center">
  <img src="https://github.com/user-attachments/assets/e0fb0299-5320-42c2-9930-3df8cd710e0c" width="45%"></img>
  &nbsp; &nbsp; &nbsp; &nbsp;
  <img src="https://github.com/user-attachments/assets/1fc3965f-3010-4641-ae0c-bb6c6d297399" width="45%"></img>
  <br><br>
  <em>Front and rear view of the control board.</em>
</div>
<br>

<br>
<div align="center">
  <img src="https://github.com/user-attachments/assets/5d92b648-7acc-413a-b1c6-34d8abe610ef" width="45%"></img>
  &nbsp; &nbsp; &nbsp; &nbsp;
  <img src="https://github.com/user-attachments/assets/be5a13e3-7623-475b-a9c3-d8398da151f8" width="45%"></img>
  <br><br>
  <em>Front and rear view of the hot plate.</em>
</div>
<br>

<br>
<div align="center">
  <img src="https://github.com/user-attachments/assets/047c66aa-6906-41f6-ba6a-bf96980a0972" width="45%"></img>
  &nbsp; &nbsp; &nbsp; &nbsp;
  <img src="https://github.com/user-attachments/assets/2eeb552f-069c-4829-87ab-ce935bd5a3fc" width="45%"></img>
  <br><br>
  <em>Front and rear view of the front panel.</em>
</div>
<br>

## Desktop Application

A GTK-based Python application (PyGObject) provides live plotting of current and target temperature, displays system state and heating stage, and allows process start/abort via USB. It can log session data to CSV and includes a device emulator using virtual serial ports (socat + pyserial) for development and testing.

<br>
<div align="center">
  <img src="https://github.com/user-attachments/assets/be5dc253-b7f2-4c92-a5d5-f75a23c24d82" width="75%"></img>
  <br><br>
  <em>Front and rear view of the front panel.</em>
</div>
<br>

## Firmware

The firmware for the reflow hot plate is developed using the STM32CubeIDE. It includes:

- Temperature control algorithm
- User interface logic
- Reflow profile management
- Safety and emergency handling

The Cube project can be found in the [Firmware](firmware/) directory.

## Gallery

<div align="center">
  <img src="https://github.com/user-attachments/assets/5577cf35-7ddc-4f20-9051-f766653a4d50" height="240">
  <img src="https://github.com/user-attachments/assets/74a66a5a-281d-488d-b156-f5e1ea3efb95" height="240">
  <img src="https://github.com/user-attachments/assets/521d3ed9-4d65-410e-be65-e40fc1e60c0c" height="240">
</div>

## Usage

1. Power on the reflow hot plate and wait for it to initialize.
1. Place your PCB with solder paste and components onto the hot plate.
1. Use the tactile buttons and OLED display to navigate through the user interface and select a reflow profile.
1. The hot plate will execute the selected reflow profile, precisely controlling the temperature to solder the components onto the PCB.
1. Once the reflow process is complete, allow the PCB to cool before removing it from the hot plate.

To visualize the temperature distribution on the heatbed, FLIR Lepton 3.5 IR camera was used.

<br>
<div align="center">
  <img width="320" height="240" alt="obraz" src="https://github.com/user-attachments/assets/d3cba5f0-dfb3-40bc-8853-9348a2d1850c" />
  <br><br>
  <em>Thermal image of the heatbed during reflow process.</em>
</div>
<br>

## Citation

If you find this project useful for your research, consider citing it using the following BibTeX entry:

```bibtex
@mastersthesis{2024:t56856,
    title="{Design and Implementation of a Reflow Hot Plate Soldering Device}",
    author="Ignacy Kajdan",
    school="Faculty of Automatic Control, Robotics & Electrical Engineering, Poznan University of Technology",
    year="2024",
    language="en",
}
```

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE.md) file for details.
