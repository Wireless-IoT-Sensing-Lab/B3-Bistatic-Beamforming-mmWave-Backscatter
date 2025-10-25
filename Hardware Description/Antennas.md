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

Mounted with its broadside facing the coverage region, a rectangular patch has wide half-power beamwidths in both principal planes (commonly on the order of $60^\circ$–$90^\circ$ depending on $W/L$ and substrate). The integral ground plane suppresses the back lobe and shields cables and electronics, so most sensitivity is directed into the *forward* hemisphere. In dense or indoor environments, multipath and angular spread further “fill in” nulls, making the azimuth response functionally omni-like for receiving while retaining the patch’s compact, low-profile form.

A small footprint does not imply a small receive aperture. Using

$$
A_e=\frac{\lambda^2 G}{4\pi},
$$

a typical broadside gain of $G\approx 6\text{–}8$ dBi yields ample effective area for robust SNR without resorting to an array—useful for $B^3$, where simplicity and repeatability matter.

---

## a 100 Ω inset feed impedance matching

We purposely set the feed point along the patch’s symmetry line where the input resistance is **about $100~\Omega$**. This choice keeps the notch relatively **shallow**, so the $TM_{10}$ current sheet is disturbed less, the landing area remains mechanically sound, and the narrower microstrip at the radiating edge adds **less capacitive loading**. In short: it’s easier to hit accurately, and it preserves the clean broad beam we want for pseudo-omni Rx.

Along the symmetry line, the input resistance varies with inset depth $y$ (measured from the radiating edge) as

$$
R_{\mathrm{in}}(y)=R_{\mathrm{edge}}\cos^{2}\!\left(\frac{\pi y}{L}\right).
$$

Solving for a $100~\Omega$ target gives a first-cut inset:

$$
y=\frac{L}{\pi}\cos^{-1}\!\sqrt{\frac{100}{R_{\mathrm{edge}}}}.
$$

Here $R_{\mathrm{edge}}$ is the resistance right at the edge ($y=0$); a quick EM model or a prior build provides a good estimate. Because the inset is shallow at $100~\Omega$, small tweaks (on the order of a millimeter for typical boards) smoothly bring $R_{\mathrm{in}}$ to target with minimal impact on resonance or pattern.

To choose the **feed and notch widths**, size the microstrip line on the same substrate for approximately $100~\Omega$ and make the slot just wide enough to admit that line without excessive fringing. For the line, use the usual microstrip relations (Hammerstad–Jensen) to relate width $W_f$ over height $h$ to $Z_0$; the effective permittivity of the line is

$$
\varepsilon_{\mathrm{eff,line}}
=\frac{\varepsilon_r+1}{2}
+\frac{\varepsilon_r-1}{2}\left(1+12\frac{h}{W_f}\right)^{-1/2}.
$$

Then select $W_f$ that realizes $Z_0\approx100~\Omega$ (invert the standard $Z_0$ formulas numerically or with a calculator), verify it clears fabrication rules, and keep the notch comparable to $W_f$ for a smooth transition into the patch.

Downstream, any external interface (e.g., a $50~\Omega$ receiver front end) can be matched with a compact printed network—quarter-wave, L-section, or broadband as bandwidth dictates—without changing the inset philosophy on the patch.

---

## Integration notes

Keep metalwork or housings at least $0.05$–$0.1\,\lambda_0$ away from the patch edges, extend the ground per the guideline above, and, after the first cut, trim $L$ slightly to recenter $f_r$. Lower $\varepsilon_r$ and moderate $h$ generally widen bandwidth and beamwidths, which helps the pseudo-omni goal; at mmWave, pay close attention to conductor roughness and dimensional tolerances, as they shift $f_r$ perceptibly.

---
