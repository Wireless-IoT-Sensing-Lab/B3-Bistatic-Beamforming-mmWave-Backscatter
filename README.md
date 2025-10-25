# B3: Bistatic Beamforming for mmWave Backscatter

This repository contains the implementation, experimental data, and hardware design files for our **Bistatic Beamforming Backscatter (B³)** system — a high-frequency mmWave tag that enables efficient beam-steered links between transmitters, receivers, and passive backscatter tags.

---

## Overview

**B3** explores bistatic beamforming techniques to enhance link robustness and energy efficiency in mmWave backscatter systems.

The repository includes:
- Hardware design files for the custom backscatter tag and RF front-end to help any researcher to reproduce this tag for their future projects
- Antenna design description for tag TX beamforming

---

## 📁 Repository Structure

| Folder | Description |
|:--|:--|
| **/hardware/** | PCB design files, RF schematics, and hardware block diagrams for the bistatic backscatter tag. |
| **/beamforming/** | MATLAB or Python scripts implementing bistatic beamforming algorithms and simulation models. |
| **/experiments/** | Raw and processed experimental data, including test configurations and simulation results. |
| **/docs/** | Documentation, design notes, and related publications. |

---

## Key Features

- **Tag Beamforming** – Coordinated TX/RX beam control for efficient tag reflection  
- **High-speed beam switching** – Up to 40 MHz hardware-supported beam switching rate  
- **Modular architecture** – Separate paths for control logic, RF front-end, and baseband processing  
- **Open research dataset** – Enables reproducibility and further development
