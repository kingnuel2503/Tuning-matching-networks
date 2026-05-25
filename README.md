# Tuning matching networks

This repository documents the design, simulation, and electromagnetic (EM) verification of two microstrip single-stub tuning networks. The circuits are designed to match a complex load impedance ($Z_L = 100 + j80\ \Omega$) to a standard $50\ \Omega$ transmission line at a design frequency of **3.2 GHz**. 

The workflow transitions from ideal analytical derivations using a Smith Chart to realistic microstrip physical layouts on a **Rogers RT/duroid 6202** substrate, validated via Keysight ADS schematic and Momentum EM simulations.

---

## Design Specifications & Substrate Properties

### Target Parameters
* **Design Frequency ($f_0$):** 3.2 GHz
* **Characteristic Impedance ($Z_0$):** $50\ \Omega$
* **Load Impedance ($Z_L$):** $100 + j80\ \Omega$ (Normalized: $z_l = 2 + j1.6$)
* **Matching Topology:** Single Shunt Stub (Open-Circuit)

### Substrate Profiles (Rogers RT/duroid 6202)
* **Relative Permittivity ($\varepsilon_r$):** 2.94
* **Substrate Thickness ($H$):** 0.127 mm (5 mils)
* **Conductor Thickness ($T$):** 0.15 mil
* **Loss Tangent ($\tan\delta$):** 0.0015

### Analytical Solution (Smith Chart)
Since a shunt topology modifies admittance, the normalized load impedance is converted to normalized load admittance:
$$\bar{y}_L = 0.3 - j0.24$$

Rotating toward the generator on the Smith Chart reveals two valid intersection points with the $1 + jb$ circle, yielding two distinct design solutions.
<img width="554" height="575" alt="image" src="https://github.com/user-attachments/assets/f4255e71-7540-4151-9840-ebae0eb9191e" />

<img width="486" height="546" alt="image" src="https://github.com/user-attachments/assets/e57dce2b-dd76-4ace-96c7-7b794d655521" />

### Design Parameters Summary

| Parameter | Circuit Solution 1 | Circuit Solution 2 |
| :--- | :--- | :--- |
| **Distance from Load ($d$)** | $0.214\lambda$ (Elec. Length: $77.04^\circ$) | $0.369\lambda$ (Elec. Length: $132.84^\circ$) |
| **Normalized Susceptance ($jb$)** | $+j1.31$ | $-j1.31$ |
| **Required Stub Admittance ($jb_{stub}$)** | $-j1.31$ | $+j1.31$ |
| **Open Stub Length ($l$)** | $0.352\lambda$ (Elec. Length: $126.72^\circ$) | $0.148\lambda$ (Elec. Length: $53.28^\circ$) |

---

## Circuit 1: $d = 0.214\lambda$, $l = 0.352\lambda$

### 1. Ideal Schematic & S-Parameters
The ideal transmission line components (`TLIN`, `TLOC`) were simulated in Keysight ADS using electrical lengths derived directly from the Smith Chart ($360^\circ \equiv \lambda$).
<img width="693" height="458" alt="image" src="https://github.com/user-attachments/assets/39e13fa7-8166-4b57-a12f-f46d454ecee3" />

* **Performance:** Achieved an ideal return loss of $dB(S_{11}) = -23.62\text{ dB}$ exactly at 3.2 GHz.
<img width="651" height="371" alt="image" src="https://github.com/user-attachments/assets/edde8f00-b74f-45c7-b073-3ad5bff4e2d4" />

### 2. Microstrip Substrate Translation
Using the LineCalc tool in ADS with the Rogers 6202 substrate properties, the electrical parameters were converted into physical dimensions. An `MTEE_ADS` component was integrated to model the physical junction of the shunt stub accurately.
<img width="702" height="403" alt="image" src="https://github.com/user-attachments/assets/c35ec29c-c766-49d7-8896-8f6b4ca5d418" />

* **Performance:** Post-tuning optimizing adjustments yielded an outstanding schematic return loss of $dB(S_{11}) = -41.62\text{ dB}$ at the design frequency.
<img width="612" height="367" alt="image" src="https://github.com/user-attachments/assets/d3751f1f-44c4-4f69-896b-a9b7b7add7d1" />

### 3. Layout & Momentum EM Co-Simulation
The layout was generated and analyzed using the ADS Momentum EM simulator to capture real-world parasitic effects, surface currents, and radiation losses.
<img width="718" height="421" alt="image" src="https://github.com/user-attachments/assets/b3caae88-adc1-4ebf-86ab-205c1149b566" />

* **EM Verification:** The EM simulation shows strong agreement with the physical schematic variables, validating deep return loss performance around the 3.2 GHz band.
<img width="624" height="347" alt="image" src="https://github.com/user-attachments/assets/40f5681b-3788-4eff-ae21-88bcc811ee1d" />

## Circuit 2: $d = 0.369\lambda$, $l = 0.148\lambda$

### 1. Ideal Schematic & S-Parameters
The second analytical branch uses a longer path to the stub position but results in a shorter open-circuit tuning stub ($l = 0.148\lambda$).
<img width="679" height="462" alt="image" src="https://github.com/user-attachments/assets/6e66162b-4983-4be2-b694-4da1bb6e78f0" />

<img width="672" height="361" alt="image" src="https://github.com/user-attachments/assets/3ebc76e2-d1a8-4b65-8729-bf8aadd03738" />

### 2. Microstrip Realization & Tuning
The circuit variables were mapped onto the microstrip elements (`MLIN`, `MLOC`, `MTEE`). Incorporating physical junction parasitics shifts the resonant frequency slightly, which was resolved by performing gradient optimization and tuning on the line lengths within ADS.
<img width="715" height="421" alt="image" src="https://github.com/user-attachments/assets/7f8dce34-ae0b-4968-a9d8-55fcc7c389e9" />

<img width="660" height="341" alt="image" src="https://github.com/user-attachments/assets/f4b47a9c-b408-4d70-ba3f-590e4a0bfa85" />

### 3. Layout & EM Validation
A full 2.5D planar electromagnetic layout simulation was conducted for Circuit 2 to verify performance against physical layout parasitics.
<img width="700" height="428" alt="image" src="https://github.com/user-attachments/assets/5c0649d8-bfd9-4f4d-abeb-5853588f93ca" />

<img width="673" height="347" alt="image" src="https://github.com/user-attachments/assets/6fed30e9-7613-42cc-ad4c-bbf01d4c9601" />

## Software Used
* **Keysight Advanced Design System (ADS):** Schematic Simulation, LineCalc, and Layout Generation.
* **ADS Momentum
