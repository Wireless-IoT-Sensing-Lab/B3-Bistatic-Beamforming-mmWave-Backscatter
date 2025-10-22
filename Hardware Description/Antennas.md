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

## Rx Antenna Design
Our initial design 
