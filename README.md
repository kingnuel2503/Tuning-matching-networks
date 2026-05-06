# Tuning matching networks

I implemented and simulated tuning circuits to match a load impedance of 100 + j80 Ω to a line with a 50 Ω characteristic impedance using single open-circuited shunt stubs design using a frequency of 3.2 GHz. I simulated two tuning circuits on Keysight ADS.
The RT/DUROID 6202 is the substrate i chose

The analytical solution is provided below using a smith chart
<img width="554" height="575" alt="image" src="https://github.com/user-attachments/assets/f4255e71-7540-4151-9840-ebae0eb9191e" />

<img width="486" height="546" alt="image" src="https://github.com/user-attachments/assets/e57dce2b-dd76-4ace-96c7-7b794d655521" />

## First Circuit
Based on calculations, the schematic of the first design is shown below. The lengths of intersection of 1 + jb circle to 
admittance and distance from stub to open circuits are obtained as 0.214 λ and 0.352λ respectively. I obtain the effective angle of TLIN and TLOC by replacing lambda as 360 degrees.

<img width="693" height="458" alt="image" src="https://github.com/user-attachments/assets/39e13fa7-8166-4b57-a12f-f46d454ecee3" />

The s-parameters of the circuit is listed below
<img width="651" height="371" alt="image" src="https://github.com/user-attachments/assets/edde8f00-b74f-45c7-b073-3ad5bff4e2d4" />

The tuned circuit and substrate properties is then taken into account
<img width="702" height="403" alt="image" src="https://github.com/user-attachments/assets/c35ec29c-c766-49d7-8896-8f6b4ca5d418" />

S-parameters of tuned circuit
<img width="612" height="367" alt="image" src="https://github.com/user-attachments/assets/d3751f1f-44c4-4f69-896b-a9b7b7add7d1" />

You can observe an improved performance in the return loss and insertion loss

### Layout and EM simulation
<img width="718" height="421" alt="image" src="https://github.com/user-attachments/assets/b3caae88-adc1-4ebf-86ab-205c1149b566" />

<img width="624" height="347" alt="image" src="https://github.com/user-attachments/assets/40f5681b-3788-4eff-ae21-88bcc811ee1d" />

## Second Circuit
For the second design, the  lengths and distance from stub to open circuits are obtained as 0.369 λ and 0.148 λ respectively

### Schematic of second design and S-parameter simulation:
<img width="679" height="462" alt="image" src="https://github.com/user-attachments/assets/6e66162b-4983-4be2-b694-4da1bb6e78f0" />

<img width="672" height="361" alt="image" src="https://github.com/user-attachments/assets/3ebc76e2-d1a8-4b65-8729-bf8aadd03738" />

### Tuned circuit and S-parameter output:
<img width="715" height="421" alt="image" src="https://github.com/user-attachments/assets/7f8dce34-ae0b-4968-a9d8-55fcc7c389e9" />

<img width="660" height="341" alt="image" src="https://github.com/user-attachments/assets/f4b47a9c-b408-4d70-ba3f-590e4a0bfa85" />

### Layout and EM simulation
<img width="700" height="428" alt="image" src="https://github.com/user-attachments/assets/5c0649d8-bfd9-4f4d-abeb-5853588f93ca" />

<img width="673" height="347" alt="image" src="https://github.com/user-attachments/assets/6fed30e9-7613-42cc-ad4c-bbf01d4c9601" />
