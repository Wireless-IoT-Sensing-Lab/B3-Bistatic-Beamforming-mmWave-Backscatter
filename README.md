#  $B^3$: Bistatic Beamforming for mmWave Backscatter

This repository provides the **implementation**, **hardware design**, and **experimental data** for the **Bistatic Beamforming Backscatter ($B^3$)** system — a high-frequency mmWave backscatter tag that enables efficient **beam-steered communication** between transmitters, receivers, and passive backscatter devices.

**📢 Please make sure to cite our paper if you use our hardware design, data, or implementation.**

Zhenzhe Lin, Chae, Yoon, Mingyo Jeong, and Parth Pathak. "B^3: Bistatic Backscatter Beamforming for mmWave IoTs" ACM SenSys 2026. 


---

##  Overview

**$B^3$** demonstrates bistatic beamforming techniques that significantly improve **link robustness**, **signal strength**, and **energy efficiency** in mmWave backscatter systems.


This repository includes:
- **Hardware design files** for the custom bistatic backscatter tag and RF front-end — allowing researchers to **reproduce or extend** the hardware design for their own projects.  
- **Hardware Description** detailing each hardware component of $B^3$. Currently detailed descriptions and simulation results of $B^3$ Tx and Rx antennas are available.


---

## 📁 Repository Structure

| Folder | Description |
|:--|:--|
| **/Hardware Description/Antennas.md** | Antenna design documentation, radiation pattern plots, and beamforming test results. |
| **/Hardware Description/Hadamard Matrix.md** | Passive Beamforming Matrix Design documentation. |
| **/PCBO/Readme-PCBO.md** | This document offers a brief description about the PCBO package. |
| **/PCBO/DOCUMENTATION/** | This directory contains the manufacturing document |
| **/PCBO/BILL OF MATERIALS/** | This directory contains the BOM document for those who want to order their own $B^3$ hardware |

---

## Key Features

- **Tag Beamforming** – Coordinated transmit/receive beam control for optimized reflection and link quality.  
- **High-Speed Beam Switching** – Hardware supports up to **40 MHz** beam-switching rate.  
- **Modular Architecture** – Clean separation of control logic, RF front-end, and baseband processing.  
- **Open and Reproducible** – Provides all design files and documents to facilitate reproducibility and future research extensions.

---


**Wireless IoT Sensing Lab**  
[George Mason University]  
[http://www.phpathak.com/]
