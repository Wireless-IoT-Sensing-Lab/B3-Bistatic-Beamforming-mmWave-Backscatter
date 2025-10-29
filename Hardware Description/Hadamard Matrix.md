# $B^3$ Hadamard Passive Beamforming Matrix Design
A Butler matrix is the most commonly used passive beamformer because it creates a single sharp raditation pattern at a differnet angle depending on the excitation port. However, the angular coverage is typically narrower and, in many in-door applications, multi-beams show  as there is significantly less chance that all main lobes are blockecd by an object. 

**4×4 Hadamard**

A Hadamard matrix generates one center beam and N-1 dual beams at two symmetric angles ($\pm\theta$). This is because the matrix creates $180^\circ$ phase differences between adjacent element groups (or elements).

$$
H_4 =
\tfrac{1}{2}
\begin{bmatrix}
1 & 1 & 1 & 1 \\
1 & -1 & 1 & -1 \\
1 & 1 & -1 & -1 \\
1 & -1 & -1 & 1
\end{bmatrix}
$$

**4×4 Butler matrix**

A Butler matrix generates a pencil beam towards N different angles depending on the excitation port. To broaden the angular coverage, it requires a larget array size. Typically Butler matrix is very hard to implement beyond N=8.

$$
\mathbf{B}_4 =
\tfrac{1}{2}
\begin{bmatrix}
1 & 1 & 1 & 1 \\
1 & \mathrm{j} & -1 & -\mathrm{j} \\
1 & -1 & 1 & -1 \\
1 & -\mathrm{j} & -1 & \mathrm{j}
\end{bmatrix}
$$

## Quadrature hybrid coupler: a building block of a passive beamformer
A **quadrature hybrid** (a 3 dB, 90° branch-line coupler) splits input power equally into two output ports with a **90° phase difference**, while ideally isolating the fourth port. As passive beamformer highly rely on electrical delay differences and power splitting within the RF PCB, a quadrature hybrid coupler is the most important component in many passive beamformers.

**Ideal behavior (port order 1→2 through, 1→3 coupled, 4 isolated):**

<p align="center">
  <a href="https://github.com/user-attachments/assets/1daf9cee-dae2-4ece-bde0-42bf00902120">
    <img height="250" alt="Quadrature hybrid coupler diagram" src="https://github.com/user-attachments/assets/ea3fad8a-58d8-445d-b14d-7813e813fbae" />
  </a><br/>
  <em>Figure 1. Quadrature hybrid (90°) coupler diagram. Source: Everything RF.</em>
</p>

$$
\mathbf{S}_\text{ideal}=\tfrac{1}{\sqrt{2}}
\begin{bmatrix}
0 & j & 1 & 0 \\
j & 0 & 0 & 1 \\
1 & 0 & 0 & j \\
0 & 1 & j & 0
\end{bmatrix}
$$

As shown in Figure 1, the four lines are **quarter-wave** sections; a common first cut uses horizontal (series) arms near $Z_0/\sqrt{2}\approx35.4~\Omega$ and vertical (shunt) arms near $Z_0\approx50~\Omega$ (final values are refined in EM to hit amplitude/phase targets). $S_{ideal}$ show the four-port S matrix that shows depending the input port, what are the two output ports and their relative phase differences.

**Quarter-wave physical length:**

$$
\ell_{90}=\frac{\lambda_g}{4}=\frac{c}{4f\sqrt{\varepsilon_\text{eff}}}
$$

As shown in Fig. 1, two $90^\circ$ traces at two different characteristic impedances ($Z_0/\sqrt{2}$, and $Z_0$) are the key design elements. Especially, at millimeter wave (mmWave) beyond 40GHz, $90^\circ$ delay lines are quite tricky to design because of the extremely short wavelength. When wavelength is very short, the $90^\circ$ lines tend to have very short length as compared to the width of the line to meet the impedance requirement. However, that causes phase inaccuracies due to the wide junctions in the vertical traces. To resolve the issue, we uses $Z_0=70.7 \Omega$.

---

**Fine-tuned Quadrature Hybrid Coupler Design**

| <a href="https://github.com/user-attachments/assets/1f7fc1f3-ea8b-4940-ac80-1be1fb2ef35a"><img height="350" alt="Figure 2. The designed microstrip quadrature hybrid coupler" src="https://github.com/user-attachments/assets/1f7fc1f3-ea8b-4940-ac80-1be1fb2ef35a" /></a> | <a href="https://github.com/user-attachments/assets/6d831ed9-ff66-4326-bbdb-1e40fa50c627"><img height="350" alt="Figure 3. The S-parameter (Magnitude)" src="https://github.com/user-attachments/assets/3b41765c-a228-4510-abbb-68e6d05edfaf" /></a> | <a href="https://github.com/user-attachments/assets/57edd651-2c44-4f71-8b04-aeb069404ad9"><img height="350" alt="Figure 4. The S-parameter (Angle) of S21 and S31" src="https://github.com/user-attachments/assets/6d049b70-5f37-4ada-a22d-b8042ef99868" /></a> |
|:--:|:--:|:--:|
| *Figure 2. Quadrature hybrid layout.*<br/>*3 dB, 90° branch-line.* | *Figure 3. S-parameter magnitude.*<br/>*\|S21\| and \|S31\| ≈ 3 dB; \|S11\|/\|S41\| show match & isolation.* | *Figure 4. S-parameter phase (S21 vs S31).*<br/>*Relative phase ≈ 90° across the band.* |

With 5-mil-thick Taconic TLX-8 substrate, line width of 0.1748mm yields the $70.7\Omega$ characteristic impedance while the $90^\circ$ trace width is around 0.85mm. The final length/height ratio is approximately 5; which is a better starting value for good $90^\circ$-phase delay design and -3dB power matching between S21 and S31. The horizontal and vertical branch 
line lengths are tuned to 0.7 and 0.75mm, respectively.

## Microstrip Crossover (using 70.7 Ω, 90° sections)

A **microstrip crossover** lets two transmission lines pass through each other on a single layer while maintaining match and isolation. One practical way at mmWave is to realize it with **$Z_0=70.7~\Omega$ quarter-wave ($90^\circ$) sections**, which provides an all-pass, single-layer structure without vias.

**Ideal 4-port behavior (1↔3, 2↔4), perfectly matched & isolated:**

$$
\mathbf{S}_\text{ideal} =
\begin{bmatrix}
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1 \\
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0
\end{bmatrix}
$$

In this ideal, **Port 1 → Port 3** and **Port 2 → Port 4** transmit with unity magnitude (and a defined reference phase), while the adjacent and opposite “non-through” ports are isolated.  
In practice, the 70.7 Ω, $\lambda_g/4$ sections set the electrical lengths so the tee/corner parasitics are absorbed into the phase budget, keeping return loss low and isolation high over the design band.

**Why 70.7 Ω and 90°?**  
The 70.7 Ω choice (i.e., $Z_0\sqrt{2}$ relative to a 50 Ω system) yields practical microstrip widths and allows the crossover to be synthesized as two quadrature paths that re-combine with the desired phase, so each line “sees” a matched through path while the orthogonal coupling is canceled.

---

**Fine-tuned microstrip crossover**

| <a href="https://github.com/user-attachments/assets/ef47e553-3f9d-4816-8d3a-24cd82cba011"><img height="350" alt="Figure 5. The designed microstrip crossover with 70.7Ω, 90° lines" src="https://github.com/user-attachments/assets/ef47e553-3f9d-4816-8d3a-24cd82cba011" /></a> | <a href="https://github.com/user-attachments/assets/ffb73675-32cf-4931-bed4-af31b649efbe"><img height="350" alt="Figure 6. S-parameters (magnitude) of the crossover" src="https://github.com/user-attachments/assets/ffb73675-32cf-4931-bed4-af31b649efbe" /></a> |
|:--:|:--:|
| *Figure 5. Microstrip crossover using $Z_0=70.7~\Omega$ quarter-wave sections.* | *Figure 6. S-parameters (magnitude): through paths (1→3, 2→4) near 0 dB with a small insertion loss; return/isolation low across the band.* |

The fine tuned crossover uses the same line width but the length was tuned to 0.84mm for a high return loss and a low insertion loss.

**Design remarks at 60 GHz:**  
Because $\lambda_g/4$ is short, the **physical $90^\circ$ length can approach pad and junction dimensions**, making the **phase extremely sensitive** to tiny geometry changes. The **70.7 Ω** target keeps line widths practical while balancing junction capacitances, helping the crossover stay matched and maintain isolation without resorting to multilayer vias.

---

## Our 4×4 Hadamard Beamformer Design

<p align="center">
  <a href="https://github.com/user-attachments/assets/50e50b09-91c7-4ba1-aac2-c0a97ddf9c74">
    <img height="600" alt="Figure 7. Final Hadamard matrix design" src="https://github.com/user-attachments/assets/50e50b09-91c7-4ba1-aac2-c0a97ddf9c74" />
  </a><br/>
  <em>Figure 7. Final Hadamard beamformer network.</em>
</p>

As shown in Fig. 7, the input ports are impedance-matched to $50~\Omega$ so the designed Hadamard network can connect to an **SP4T (single-pole, four-throw)** RF switch with lower mismatch loss. The output nodes are kept at $70.7~\Omega$ because the antenna is matched to $70.7~\Omega$. The transmission lines in each stage are fine-tuned to realize the target phase distributions. However, due to the impedance sensitivity of the quadrature hybrid coupler, avoiding impedance and phase imbalance is challenging and the tuning requires extensive EM simulations. Our final tuned S-parameter results are below.

---

### Port 1 excitation

| <a href="https://github.com/user-attachments/assets/39da352a-135a-4feb-a7c8-26a1ae7a1d36"><img height="300" alt="Figure 8. S-parameters (magnitude) at Port 1 excitation" src="https://github.com/user-attachments/assets/39da352a-135a-4feb-a7c8-26a1ae7a1d36" /></a> | <a href="https://github.com/user-attachments/assets/f6167672-8a27-4555-aa94-34bc9b3dc9fe"><img height="300" alt="Figure 9. S-parameters (angle) at Port 1 excitation" src="https://github.com/user-attachments/assets/f6167672-8a27-4555-aa94-34bc9b3dc9fe" /></a> |
|:--:|:--:|
| *Figure 8. S-parameters (magnitude), Port 1 excitation.* | *Figure 9. S-parameters (angle), Port 1 excitation.* |

### Port 2 excitation

| <a href="https://github.com/user-attachments/assets/ef67fb25-baa7-44d0-bc15-5e74a19fe3b7"><img height="300" alt="Figure 10. S-parameters (magnitude) at Port 2 excitation" src="https://github.com/user-attachments/assets/ef67fb25-baa7-44d0-bc15-5e74a19fe3b7" /></a> | <a href="https://github.com/user-attachments/assets/c1f02e03-8fff-4497-82d7-eeee9d60953a"><img height="300" alt="Figure 11. S-parameters (angle) at Port 2 excitation" src="https://github.com/user-attachments/assets/c1f02e03-8fff-4497-82d7-eeee9d60953a" /></a> |
|:--:|:--:|
| *Figure 10. S-parameters (magnitude), Port 2 excitation.* | *Figure 11. S-parameters (angle), Port 2 excitation.* |

### Port 3 excitation

| <a href="https://github.com/user-attachments/assets/45a648ec-caec-4e7a-bd6a-d19dc9783381"><img height="300" alt="Figure 12. S-parameters (magnitude) at Port 3 excitation" src="https://github.com/user-attachments/assets/45a648ec-caec-4e7a-bd6a-d19dc9783381" /></a> | <a href="https://github.com/user-attachments/assets/b7577b24-5453-41a5-850d-784c350be147"><img height="300" alt="Figure 13. S-parameters (angle) at Port 3 excitation" src="https://github.com/user-attachments/assets/b7577b24-5453-41a5-850d-784c350be147" /></a> |
|:--:|:--:|
| *Figure 12. S-parameters (magnitude), Port 3 excitation.* | *Figure 13. S-parameters (angle), Port 3 excitation.* |

### Port 4 excitation

| <a href="https://github.com/user-attachments/assets/426ba518-2663-4fc4-be7c-9da0dda3d2d7"><img height="300" alt="Figure 14. S-parameters (magnitude) at Port 4 excitation" src="https://github.com/user-attachments/assets/426ba518-2663-4fc4-be7c-9da0dda3d2d7" /></a> | <a href="https://github.com/user-attachments/assets/dfd6607b-c0a3-42eb-adc8-a2b0f24ce42b"><img height="300" alt="Figure 15. S-parameters (angle) at Port 4 excitation" src="https://github.com/user-attachments/assets/dfd6607b-c0a3-42eb-adc8-a2b0f24ce42b" /></a> |
|:--:|:--:|
| *Figure 14. S-parameters (magnitude), Port 4 excitation.* | *Figure 15. S-parameters (angle), Port 4 excitation.* |

**Summary at 60 GHz:** The simulated phase imbalance is approximately within $5^\circ$ at 60 GHz (worst case), and the typical amplitude imbalance is within **1.0 dB** at 60 GHz.
