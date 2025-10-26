# $B^3$ Antenna Designs
Wide beam-coverage is the key factor of successful deployment of $B^3$. For a broader beam coverage and faster beam searching, we choose 4X4 Hadamard beamforming matrix.

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

When a four-linear array antenna is fed by a passive Hadamard beamforming matrix that has the voltage and phase distribution as $H_4$, the array antenna could generate four beam patterns with one center beam and three dual split-beams at two symmetric angles $\pm\theta$.

This document focus on sharing design details of the array antennas we designed for $B^3$. The design of a passive Hadamard beamforming network will be discussed in a separate document.

# Rx Antenna Design

This chapter describes the receive (Rx) antenna used in $B^3$: a single rectangular microstrip patch operating in $TM_{10}$. The choice is deliberate—compared with small arrays it occupies less area, is easy to integrate above a solid ground, and, when pointed broadside at the service region, exhibits a wide, smooth main lobe that behaves like a **pseudo-omnidirectional** pattern for reception.

---

## Electromagnetic model and first-cut dimensions

The patch is treated as a resonant $TM_{10}$ cavity with fringing fields at the radiating edges. Standard closed-form formulas provide a reliable starting point (SI units).

**Patch width (broadside gain and bandwidth improve with larger $W$):**

$$
W=\frac{c}{2f_r}\sqrt{\frac{2}{\varepsilon_r+1}}
$$

**Effective permittivity (accounts for fringing into air):**

$$
\varepsilon_{\mathrm{eff}}
=\frac{\varepsilon_r+1}{2}
+\frac{\varepsilon_r-1}{2}\left(1+12\frac{h}{W}\right)^{-1/2}
$$

**Fringing length extension (per edge):**

$$
\Delta L
=0.412\,h\;
\frac{\left(\varepsilon_{\mathrm{eff}}+0.3\right)\left(\frac{W}{h}+0.264\right)}
{\left(\varepsilon_{\mathrm{eff}}-0.258\right)\left(\frac{W}{h}+0.8\right)}
$$

**Effective and physical length (sets the resonance):**

$$
L_{\mathrm{eff}}=\frac{c}{2f_r\sqrt{\varepsilon_{\mathrm{eff}}}}
$$

$$
L=L_{\mathrm{eff}}-2\Delta L
$$

**Ground plane sizing (keeps the pattern stable):**

$$
W_g \gtrsim W+6h,\qquad L_g \gtrsim L+6h
$$

*Symbols:* $c$ speed of light; $\varepsilon_r$ substrate relative permittivity; $h$ substrate thickness; $W,L$ patch width/length; $f_r$ target resonance.

---

## Why a single patch is a good pseudo-omni **receiver**

Mounted with its broadside facing the coverage region, a rectangular patch has wide half-power beamwidths in both principal planes (commonly on the order of $60^\circ$ – $90^\circ$ depending on $W/L$ and substrate). The integral ground plane suppresses the back lobe and shields cables and electronics, so most sensitivity is directed into the *forward* hemisphere. In dense or indoor environments, multipath and angular spread further “fill in” nulls, making the azimuth response functionally omni-like for receiving while retaining the patch’s compact, low-profile form.

A small footprint does not imply a small receive aperture. Using

$$
A_e=\frac{\lambda^2 G}{4\pi},
$$

a typical broadside gain of $G\approx 6\text{–}8$ dBi yields ample effective area for robust SNR without resorting to an array—useful for $B^3$, where simplicity and repeatability matter.

---

## a 100 Ω inset feed impedance matching

We purposely set the feed point along the patch’s symmetry line where the input resistance is **about $100~\Omega$**. This choice keeps the notch relatively **shallow**, so the $TM_{10}$ current sheet is disturbed less, and the narrower microstrip at the radiating edge adds **less capacitive loading**. Therefore, it preserves the clean broad beam we want for pseudo-omni Rx.

Along the symmetry line, the input resistance varies with inset depth $y$ (measured from the radiating edge) as

$$
R_{\mathrm{in}}(y)=R_{\mathrm{edge}}\cos^{2}\\left(\frac{\pi y}{L}\right).
$$

Solving for a $100~\Omega$ target gives a first-cut inset:

$$
y=\frac{L}{\pi}\cos^{-1}\\sqrt{\frac{100}{R_{\mathrm{edge}}}}.
$$

Here $R_{\mathrm{edge}}$ is the resistance right at the edge ($y=0$); a quick EM model or a prior build provides a good estimate. Because the inset is shallow at $100~\Omega$, small tweaks (on the order of a millimeter for typical boards) smoothly bring $R_{\mathrm{in}}$ to target with minimal impact on resonance or pattern.

To choose the **feed and notch widths**, size the microstrip line on the same substrate for approximately $100~\Omega$ and make the slot just wide enough to admit that line without excessive fringing. For the line, use the usual microstrip relations (Hammerstad–Jensen) to relate width $W_f$ over height $h$ to $Z_0$; the effective permittivity of the line is

$$
\varepsilon_{\mathrm{eff,line}}
=\frac{\varepsilon_r+1}{2}
+\frac{\varepsilon_r-1}{2}\left(1+12\frac{h}{W_f}\right)^{-1/2}.
$$

We chose the inset with the same as 100-ohm trace width ($W_{100Ω}$) and fine-tuned the inset length so that we have impedance matching at 100Ω. Then, using a quarter-wave transformer, 50Ω impedance matching was implemented.

---

## The fine-tuned Rx antenna design

| <a href="https://github.com/user-attachments/assets/20760015-aa49-41a0-b14a-b6fbbe27c5c2"><img src="https://github.com/user-attachments/assets/20760015-aa49-41a0-b14a-b6fbbe27c5c2" alt="Rx Antenna" height="400"></a> | <a href="https://github.com/user-attachments/assets/3bfa50a5-b682-4d31-af23-55340dbb59ba"><img src="https://github.com/user-attachments/assets/3bfa50a5-b682-4d31-af23-55340dbb59ba" alt="Rx Antenna S11" height="400"></a> |
|:--:|:--:|
| *Figure 1. Rx antenna (rectangular microstrip patch).* | *Figure 2. Return loss (S11) of the Rx patch).* |

Fig. 1 shows the finalized Rx microstrip patch antenna with 100Ω-line inset match and it shows a impedance bandwidth of approximately 2GHz (59.2-61.2GHz) which corresponds to a 3.33% fractional bandwidth.

### Design summary and parameters
The fine-tuned design parameters are itemmized and listed below.

**Substrate:** Taconic TLX-8, 5 mil (0.127 mm) core.

**Patch geometry:**  
- Patch width $W_{\text{patch}} = 1.87$ mm  
- Patch length (height) $H_{\text{patch}} = 1.45$ mm  

**Inset feed (100 Ω target at the feed point):**  
- Inset width $W_{\text{inset}} = W_{100\Omega} = 0.0762$ mm  
- Inset depth $H_{\text{inset}} = 0.4$ mm  
rent sheet, and reduces capacitive loading at the radiating edge—helpful for preserving a broad, smooth receive pattern (pseudo-omni) while maintaining a robust landing area.

**Microstrip lines on TLX-8 (same stackup)**  
Each listed length is a 90° electrical length (i.e., $\lambda_g/4$) at the design frequency for that microstrip line width.

| Line Impedance | Width (mm) | Length for 90° (mm) |
|:--:|:--:|:--:|
| $100~\Omega$ | **0.0762** | **0.895** |
| $70.7~\Omega$ | **0.1745** | **0.8725** |
| $50~\Omega$ | **0.33** | **0.8517** |

### Far-field performance

| <a href="https://github.com/user-attachments/assets/149b7673-c69e-4aa8-9812-db17473b345e"><img height="400" alt="Rx antenna far-field radiation pattern at 60GHz" src="https://github.com/user-attachments/assets/149b7673-c69e-4aa8-9812-db17473b345e" /></a> | <a href="https://github.com/user-attachments/assets/3228c77c-a41b-43cc-a67c-5e6e0dabcde0"><img height="400" alt="Rx antenna peak realized gain over frequency" src="https://github.com/user-attachments/assets/3228c77c-a41b-43cc-a67c-5e6e0dabcde0" /></a> |
|:--:|:--:|
| *Figure 3. Rx antenna far-field radiation pattern at 60 GHz.* | *Figure 4. Rx antenna peak realized gain versus frequency.* |

The fine-tuned Rx antenna shows the peak realized gain of 7.83dBi at 60GHz and the Realize gain is above 6.5dBi within the impedance bandwidth. This allows the tag can be reachable by a distant nodes while allowing a moderate angular beam covereage.


# Tx Antenna Array Final Design

While Rx antenna requires pseudo-omni-directional operation, a $B^3$ Tx antenna requres higher gain as wider and selected beam. For the goal of $B^3$, a Hadamard linear switched array antenna is a perfect choice as it offers much wider beam coverage with high gain. Using the Rx antenna's dimensions as a starting point, the array antenna is tuned. For a compact design, we limited the liear array size to 4, while each element is a 4X1 series patch antenna array to maximize the gain for a long distance communication. The 4X4 array antenna was fine-tuned using CST Microwave Studio 2025 time domain solver. The element to element spacing (3.131mm) is equal to a guided-wavelength in a 5-mils-thick Taconic TLX-8 substrate. The physical spacing is also corresponding to a 0.63 free space wavelength, which offers a moderate gain as well as moderate grating lobe rejection.

## 4X1 Subarray element

| <a href="https://github.com/user-attachments/assets/dcec094f-dd77-4e3d-b643-cf9723ec8e4e"><img height="400" alt="Figure 5. The fine-tuned 4×4 array antenna design" src="https://github.com/user-attachments/assets/dcec094f-dd77-4e3d-b643-cf9723ec8e4e" /></a> | <a href="https://github.com/user-attachments/assets/6ad3ba4c-07f6-4187-838d-056588f62e03"><img height="400" alt="Figure 6. The simulated far-field radiation pattern of a linear 4×1 patch array element in the 4×4 array antenna" src="https://github.com/user-attachments/assets/6ad3ba4c-07f6-4187-838d-056588f62e03" /></a> |
|:--:|:--:|
| *Figure 5. The fine-tuned 4×4 array antenna design.* | *Figure 6. Simulated far-field radiation pattern of a linear 4×1 patch array element within the 4×4 array.* |

<p align="center">
  <a href="https://github.com/user-attachments/assets/e789543e-79c1-4c7d-8468-cfeab6352358">
    <img height="400" alt="Figure 7. Reflection coefficient of 4×1 patch array element" src="https://github.com/user-attachments/assets/e789543e-79c1-4c7d-8468-cfeab6352358" />
  </a><br/>
  <em>Figure 7. Reflection coefficient of a 4×1 patch array element.</em>
</p>

The fine-tuned antenna subarray is designed with a 100Ω feed line with 0.9mm feed line length which points beam towards the lower elevation angle for a good impedance matching within the operating frequency. The nominal patch antenna size is decided $(W_{patch_{norm}}, H_{patch_{norm}})$ = (1.87, 1.45) [mm]. And the width ratio for the each element within the subarray is tuned to be (0.8, 1, 1, 0.8) while 1 corresponds to $W_{patch_{norm}}$. As a result, the sub-array has almost 10% fractional bandwidth (6GHz impedance bandwidth from 57.15GHz to 63.24GHz). The subarray peak realized gain is approximately 10.8dBi.

## 4X4 Tx Linear Array Simulation Result

| <a href="https://github.com/user-attachments/assets/af10bab1-baf5-4497-9209-0f0cea8df004"><img width="557" height="450" alt="$B^3$ Tx switched array final design" src="https://github.com/user-attachments/assets/af10bab1-baf5-4497-9209-0f0cea8df004" /></a> | <a href="https://github.com/user-attachments/assets/3243bb02-bac7-429b-8c7f-00495b132f20"><img width="1208" height="450" alt="Reflection coefficient of the Tx antenna" src="https://github.com/user-attachments/assets/3243bb02-bac7-429b-8c7f-00495b132f20" /></a> |
|:--:|:--:|
| *Figure 8. $B^3$ Tx switched-array final design.* | *Figure 9. Reflection coefficient (S11) of the Tx antenna.* |

We integrated the designed microstrip 4X4 Hadamard matrix passive beamforming matrix and the 4X4 linear patch array antenna so that we can switch beams electrically for the demonstration of $B^3$. The impedance bandwidth of the final araay is similar to that of the linear array element but slightly wider. Now, depending on which input port we excite the RF signal, Hadamard beamformer generates four different beam shapes as below.

| <a href="https://github.com/user-attachments/assets/e8b0e049-3c50-40f7-9efa-925ca538c30a"><img width="1241" height="450" alt="$B^3$ Tx beam pattern 1" src="https://github.com/user-attachments/assets/e8b0e049-3c50-40f7-9efa-925ca538c30a" /></a> | <a href="https://github.com/user-attachments/assets/f2b9e04a-1b89-46d9-85ee-22951b230ed9"><img width="1241" height="450" alt="$B^3$ Tx beam pattern 2" src="https://github.com/user-attachments/assets/f2b9e04a-1b89-46d9-85ee-22951b230ed9" /></a> |
|:--:|:--:|
| *Figure 10. B^3 Tx beam pattern 1.* | *Figure 11. B^3 Tx beam pattern 2.* |

| <a href="https://github.com/user-attachments/assets/9cbb3155-705d-4107-b4fe-1506d67907a0"><img width="1242" height="450" alt="$B^3$ Tx beam pattern 3" src="https://github.com/user-attachments/assets/9cbb3155-705d-4107-b4fe-1506d67907a0" /></a> | <a href="https://github.com/user-attachments/assets/580e1c96-9047-4385-9211-b26c9513bb8c"><img width="1239" height="450" alt="$B^3$ Tx beam pattern 4" src="https://github.com/user-attachments/assets/580e1c96-9047-4385-9211-b26c9513bb8c" /></a> |
|:--:|:--:|
| *Figure 12. B^3 Tx beam pattern 3.* | *Figure 13. B^3 Tx beam pattern 4.* |

The 4th beam pattern is the center beam and this beam patterns is created when the phase output of the beamformer is the same for all 4 output ports. Then 1st, 2nd, and 3rd beams have two main lobes and the beam pattern is symmetric to the broadside. The peak gain at beam#4 is approximately 14.6dBi at 60GHz (15.5dBi @ 62.5GHz), and the split beams have approximately 3dB lower gain.
