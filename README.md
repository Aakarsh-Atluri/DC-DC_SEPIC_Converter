# SEPIC Converter: Hardware Design and Implementation

![Status](https://img.shields.io/badge/Status-Completed-success)
![Institution](https://img.shields.io/badge/Institution-IIT_Indore-blue)

Hardware implementation of a Single-Ended Primary-Inductor Converter (SEPIC) designed to operate in both buck and boost modes. This repository contains the project report, hardware design notes, and waveform analysis for operation in both Continuous Conduction Mode (CCM) and Discontinuous Conduction Mode (DCM).

##  Team Members
- **Aakarsh Atluri** (240002014) 
- **Chukka Hemanth Kumar Naidu** (240002021)
- **Kavya Jigarkumar Shah** (240002029)
- **Nagalla Abhisri Karthik** (240002041)

_Department of Electrical Engineering, Indian Institute of Technology Indore (IITI)_

---

## Project Specifications

| Parameter | Value |
| :--- | :--- |
| **Input Voltage** | 15 V |
| **Output Voltage Range** | 10 V - 20 V |
| **Switching Frequency** | 5 kHz |
| **Target Output Current** | 1 A |
| **Operating Modes** | Buck, Boost (CCM & DCM) |

---

## Working Principle

A Single-Ended Primary Inductor Converter (SEPIC) allows the output voltage to be either greater or less than the input voltage. This topology ensures a smooth, **non-inverted** output voltage. It consists of two inductors, two capacitors, a diode, and a switching MOSFET.

- **ON State:** The MOSFET is activated, and both inductors store energy.
- **OFF State:** The MOSFET is deactivated, and the stored energy in the inductors is transferred to the output capacitor and the load.

---

## Hardware Setup

The physical prototype is divided into two main stages to isolate the control logic from the high-current power paths:

1. **PWM Controller (TL494):** - The control module is based on the **TL494** bootstrapping IC. 
   - It generates PWM signals with a variable frequency and duty cycle. These signals provide gate pulses to the converter, allowing precise control of the output voltage (through adjusting the duty cycle) and the operation mode (through adjusting the switching frequency).

2. **Gate Driver Circuit:** - Utilizes the **TC4428A** MOSFET driver to safely and efficiently drive the switching MOSFETs in the converter, ensuring sharp, clean gate pulses.

3. **Power Stage (Perfboard):** - The main SEPIC topology is point-to-point soldered on a perfboard to minimize parasitic inductance and ground bounce.
   - **Switch (MOSFET):** **IRFZ44N** Power MOSFET
   - **Power Diode:** QH08TZ600
   - **Inductors (L1, L2):** 1mH Toroidal Inductors (Bourns 2324-H-RC2342)
   - **Coupling & Output Filter (C1, C2):** 220µF Electrolytic Capacitors

---

## Results and Analysis

### 1. Voltage Regulation
The converter successfully demonstrated both step-down and step-up capabilities using a 15V DC input:
- **Buck Mode (D < 0.5):** Achieved an output of **8.13 V** at a 40% duty cycle.
- **Boost Mode (D > 0.5):** Achieved an output of **16.78 V** at a 54% duty cycle.

### 2. Operating Modes (CCM vs. DCM)
- **Continuous Conduction Mode (CCM):** Utilizing a standard high-wattage rheostat load (~15-20Ω), the switch current and diode voltage waveforms were captured, demonstrating a continuous "shark fin" inductor current with no zero-current intervals.
- **Discontinuous Conduction Mode (DCM):** By significantly increasing the load resistance, the energy demand dropped, successfully forcing the inductor current into DCM. This was verified via the broken triangular waveforms on the oscilloscope, highlighting the severe voltage gain shift inherent to DCM.

---

## Hardware Design & Prototyping Notes

For students or engineers attempting to recreate this circuit, note the following physical constraints:
- **Avoid Breadboards for Power:** Initial open-loop testing on breadboards can cause violent LC resonance and destructive voltage spikes due to stray inductance. Always move the high-current loop (Input Cap -> MOSFET -> Coupling Cap -> Diode) to a soldered perfboard or PCB as early as possible.
- **Gate Drive Integrity:** Do not attempt to drive the IRFZ44N directly with a standard 5V logic signal. Ensure the TC4428A driver swings the gate fully to 10V-12V to fully enhance the MOSFET and avoid massive thermal dissipation in the linear region.
- **Ground Separation:** The power stage ground and the logic/function generator ground should only meet at a single "Star Point" (ideally at the MOSFET Source pin) to prevent switching noise from resetting the control ICs.

---

