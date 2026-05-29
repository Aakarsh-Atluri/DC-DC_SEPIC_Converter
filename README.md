---

## 📊 Results and Analysis

### 1. Voltage Regulation
The converter successfully demonstrated both step-down and step-up capabilities using a 15V DC input:
* **Buck Mode ($D < 0.5$):** Achieved an output of **8.13 V** at a 40% duty cycle.
* **Boost Mode ($D > 0.5$):** Achieved an output of **16.78 V** at a 54% duty cycle.

### 2. Operating Modes (CCM vs. DCM)
* **Continuous Conduction Mode (CCM):** Utilizing a standard high-wattage rheostat load (~15-20Ω), the switch current and diode voltage waveforms were captured, demonstrating a continuous "shark fin" inductor current with no zero-current intervals.
* **Discontinuous Conduction Mode (DCM):** By significantly increasing the load resistance, the energy demand dropped, successfully forcing the inductor current into DCM. This was verified via the broken triangular waveforms on the oscilloscope, highlighting the severe voltage gain shift inherent to DCM.

---

## 💡 Hardware Design & Prototyping Notes

For students or engineers attempting to recreate this circuit, note the following physical constraints:
* **Avoid Breadboards for Power:** Initial open-loop testing on breadboards can cause violent LC resonance and destructive voltage spikes due to stray inductance. Always move the high-current loop (Input Cap -> MOSFET -> Coupling Cap -> Diode) to a soldered perfboard or PCB as early as possible.
* **Gate Drive Integrity:** Do not attempt to drive the IRFZ44N directly with a standard 5V logic signal. Ensure the gate drive signal swings fully to 10V-12V to fully enhance the MOSFET and avoid massive thermal dissipation in the linear region.
* **Ground Separation:** The power stage ground and the logic/function generator ground should only meet at a single "Star Point" (ideally at the MOSFET Source pin) to prevent switching noise from resetting the control IC.

---
*Documentation derived from B1 Group 6 Power Electronics Lab Report.*
