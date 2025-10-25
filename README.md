#  B3: Bistatic Beamforming for mmWave Backscatter

This repository provides the **implementation**, **hardware design**, and **experimental data** for the **Bistatic Beamforming Backscatter (B3)** system — a high-frequency mmWave backscatter tag that enables efficient **beam-steered communication** between transmitters, receivers, and passive backscatter devices.

---

##  Overview

**B3** demonstrates bistatic beamforming techniques that significantly improve **link robustness**, **signal strength**, and **energy efficiency** in mmWave backscatter systems.

This repository includes:
- **Hardware design files** for the custom bistatic backscatter tag and RF front-end — allowing researchers to **reproduce or extend** the hardware design for their own projects.  
- **Antenna design documentation** detailing the tag’s **transmit beamforming** and test configurations.

---

## 📁 Repository Structure

| Folder | Description |
|:--|:--|
| **/Hardware Description/Antennas.md/** | Antenna design documentation, radiation pattern plots, and beamforming test results. |
| **/PCBO/Readme-PCBO.md/** | Step-by-step instructions for reproducing the PCB design and submitting fabrication orders. |
| **/PCBO/B³_FINAL_OUTPUT.7z/** | Compressed archive containing PCB layout files, Gerber and DXF files, documentation, and the full Bill of Materials (BOM). |

---

## ⚙️ Key Features

- **Tag Beamforming** – Coordinated transmit/receive beam control for optimized reflection and link quality.  
- **High-Speed Beam Switching** – Hardware supports up to **40 MHz** beam-switching rate.  
- **Modular Architecture** – Clean separation of control logic, RF front-end, and baseband processing.  
- **Open and Reproducible** – Provides all design files and documents to facilitate reproducibility and future research extensions.

---



**Wireless IoT Sensing Lab**  
[George Mason University]  
[http://www.phpathak.com/]
