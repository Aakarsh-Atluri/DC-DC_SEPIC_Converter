# SEPIC Converter: Hardware Design and Implementation

![Status](https://img.shields.io/badge/Status-Completed-success)
![Institution](https://img.shields.io/badge/Institution-IIT_Indore-blue)

Hardware implementation of a Single-Ended Primary-Inductor Converter (SEPIC) designed to operate in both buck and boost modes. This repository contains the project report, hardware design notes, and waveform analysis for operation in both Continuous Conduction Mode (CCM) and Discontinuous Conduction Mode (DCM).

## 👥 Team Members
- **Aakarsh Atluri** (240002014) 
- **Chukka Hemanth Kumar Naidu** (240002021)
- **Kavya Jigarkumar Shah** (240002029)
- **Nagalla Abhisri Karthik** (240002041)

_Department of Electrical Engineering, Indian Institute of Technology Indore (IITI)_

---

## ⚡ Project Specifications

| Parameter | Value |
| :--- | :--- |
| **Input Voltage** | 15 V |
| **Output Voltage Range** | 10 V - 20 V |
| **Switching Frequency** | 5 kHz |
| **Target Output Current** | 1 A |
| **Operating Modes** | Buck, Boost (CCM & DCM) |

---

## 🛠️ Hardware Setup

The physical prototype is divided into two main stages to isolate control logic from high-current power paths:

1. **Gate Driver Circuit:** Utilizes a TC442X-based driver board (EMPEL_IITI V_3.1) to ensure sharp, clean gate pulses (0V to >10V) for optimal MOSFET switching.
2. **Power Stage (Perfboard):** The main SEPIC topology is point-to-point soldered on a perfboard. This minimizes parasitic inductance and ground bounce compared to plastic breadboards, ensuring safe operation at 1A.
    - **Switch:** IRFZ44N Power MOSFET (with 10kΩ gate pull-down)
    - **Inductors:** 1mH Toroidal Inductors (L1, L2)
    - **Coupling & Output Filter:** 220µF Capacitors

---

## 📊 Results and Analysis

### 1. Voltage Regulation
The converter successfully demonstrated both step-down and step-up capabilities using a 15V DC input:
- **Buck Mode (D < 0.5):** Achieved an output of **8.13 V** at a 40% duty cycle.
- **Boost Mode (D > 0.5):** Achieved an output of **16.78 V** at a 54% duty cycle.

### 2. Operating Modes (CCM vs. DCM)
- **Continuous Conduction Mode (CCM):** Utilizing a standard high-wattage rheostat load (~15-20Ω), the switch current and diode voltage waveforms were captured, demonstrating a continuous "shark fin" inductor current with no zero-current intervals.
- **Discontinuous Conduction Mode (DCM):** By significantly increasing the load resistance, the energy demand dropped, successfully forcing the inductor current into DCM. This was verified via the broken triangular waveforms on the oscilloscope, highlighting the severe voltage gain shift inherent to DCM.

---

## 💡 Hardware Design & Prototyping Notes

For students or engineers attempting to recreate this circuit, note the following physical constraints:
- **Avoid Breadboards for Power:** Initial open-loop testing on breadboards can cause violent LC resonance and destructive voltage spikes due to stray inductance. Always move the high-current loop (Input Cap -> MOSFET -> Coupling Cap -> Diode) to a soldered perfboard or PCB as early as possible.
- **Gate Drive Integrity:** Do not attempt to drive the IRFZ44N directly with a standard 5V logic signal. Ensure the gate drive signal swings fully to 10V-12V to fully enhance the MOSFET and avoid massive thermal dissipation in the linear region.
- **Ground Separation:** The power stage ground and the logic/function generator ground should only meet at a single "Star Point" (ideally at the MOSFET Source pin) to prevent switching noise from resetting the control IC.

---
