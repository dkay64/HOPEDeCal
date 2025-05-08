# HeliCAL Project

**Authors**  
- Jacob Gottesman  
- Dhruv Kesavarap  
- Myint Shein Hein  

## Overview

This repository contains all design and supporting files for the **HeliCAL Project**, a PCB “hat” for the NVIDIA Jetson Nano that offloads real-time hardware tasks to an ESP32. The primary objective is to enable accurate encoder tracking and reliable PWM control through UART communication, addressing hardware-timer and interrupt limitations on the Jetson Nano.

---

## Project Rationale

### Why Use an ESP32 with a Jetson Nano?
- **Precise Timing**: The Jetson Nano does not provide robust hardware timers for high-speed, deterministic tasks.
- **Reliable Interrupt Handling**: Real-time interrupt-driven tasks like counting encoder ticks or generating precise PWM signals can be offloaded to the ESP32.
- **Efficient I2C/UART Integration**: The ESP32 communicates critical data and signals back to the Jetson Nano over UART or I2C, letting the Nano focus on higher-level tasks such as sensor fusion or machine learning inference.

### System Impact
- This PCB is **crucial** for achieving fine-grained positional control and motion tracking.
- It augments the Jetson Nano by providing dedicated hardware resources, ensuring consistent performance in time-sensitive control loops.

---

## Features

- **ESP32 I2C Slave**: Handles encoders (up to five quadrature encoders), limit switches, and PWM generation.
- **Compact “Hat” Form Factor**: Designed to match the Jetson Nano footprint, stacking headers for direct mounting.
- **External Connections**: 
  - **Limit Switches** (six digital inputs), 
  - **Encoders** (five quadrature interfaces), 
  - **PWM Outputs** (for motor drivers).
- **JST SH Connectors**: Easy plug-and-play for limit switches and encoders.
- **I2C Header**: Standard interface to the Jetson Nano.

---

## Repository Structure

[ADD LATER]

- **Drill Files/**: Contains drill data for PCB fabrication.
- **HeliCALSymbols/**: Custom schematic symbols for KiCad or other EDA tools.
- **Libraries/**: Library files for standard components or footprints.
- **Project/**: Main project files (schematic, PCB layout, settings, etc.).
- **DFM analysis report_JLCDFM_Drill Files.pdf**: Manufacturer’s Design for Manufacturing (DFM) analysis report for the drill files.
- **Drill Files.zip**: Compressed set of all drill files.
- **HeliCAL-Project.zip**: Complete project archive (schematic, layout, BOM).

---

## Getting Started

1. **Clone or Download** this repository.
2. **Unzip** the `HeliCAL-Project.zip` if you plan to open the schematic and PCB layout in your preferred EDA tool (e.g., KiCad).
3. **Install Dependencies** (if needed):
   - [KiCad 9](https://www.kicad.org/) (or whichever EDA tool is used).
   - [ESP-IDF](https://github.com/espressif/esp-idf) or [Arduino Core for ESP32](https://github.com/espressif/arduino-esp32) (for firmware).

4. **Open the Project Files**:
   - Schematic: Within the `Project/` directory (or extracted folder from `HeliCAL-Project.zip`).
   - PCB Layout: Same directory, typically `.kicad_pcb` or equivalent.

---

## Documentation

### 1. Project Overview
- The **Project Overview** and objective can be found in the following [Design Documentation](https://docs.google.com/document/d/1W3Rr75G_mAyZYp311O1N4kCC289wXiKfa5qg6Yp5ShQ/edit?usp=sharing).
- Focuses on enhancing the Jetson Nano’s real-time capabilities using an ESP32 as an I2C/UART slave microcontroller.

### 2. Scope
- Covers the **PCB design**, **fabrication**, and **software implementation** for the ESP32 on the Jetson Nano.
- **Excludes** higher-level software application layers, enclosure designs, and robust thermal management beyond ensuring adequate component ratings.

### 3. PCB Block Diagram
A conceptual **PCB Block Diagram** (NOT YET INCLUDED AS A SEPARATE IMAGE HERE) outlines:
- **Jetson Nano** connections (5V Power, I2C, UART, etc.).
- **ESP32** module for interrupts and real-time control.
- **Connectors** for encoders, limit switches, PWM outputs.

### 4. Design Details
- **Why**: Jetson Nano’s limited interrupt handling and timer features.
- **Where**: The board sits as a hat on the Jetson Nano, powered by 5V from the Nano itself.
- **What**: 
  - Precise PWM generation for DC motor drivers.
  - Encoder inputs captured via dedicated ESP32 hardware timers.
  - I2C OR UART communication for data exchange with the Nano.

### 5. Specifications
- **Voltage**: 5V from Jetson Nano.
- **Current**: Dependent on external loads for motors, sensors, etc. The ESP32 itself draws ~240 mA max, depending on Wi-Fi/Bluetooth usage (though not primary in this design).
- **Encoders**: Up to five channels, quadrature signals.
- **Limit Switches**: Six digital inputs.
- **PWM**: Multiple output channels to drive external motor controllers.

### 6. Design Trade-offs
- **Buck vs. Linear Regulation**: Decided to rely on Jetson Nano’s 5V supply for simplicity and minimal heat generation on-board.
- **Pin Count**: JST SH connectors chosen to save space; trade-off is smaller pitch, requiring careful assembly.

### 7. Bill of Materials (BOM)
- A detailed **BOM** is provided in the `Project/` directory and in the main design files. It includes:
  - ESP32 module
  - JST SH connectors
  - Stacking headers for Jetson Nano
  - Support components (resistors, capacitors, level shifters if needed)


---

## License
This project is released under [MIT License](LICENSE) (or indicate whichever license you prefer). Please see the `LICENSE` file for more details.

---

## References & Appendices
- **Datasheets**:  
  - [ESP32](https://www.espressif.com/en/products/socs/esp32)
  - [INSERT MPU AND OTHER RELEVANT DATASHEETS]
  - Relevant JST SH connector datasheets
- **Design Files**:  
  - Schematic & PCB layout in `Project/` and `HeliCAL-Project.zip`.
- **Testing Logs**:  
  - See `DFM analysis report_JLCDFM_Drill Files.pdf` for manufacturer feedback.
