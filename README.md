# Two-Stage Miller-Compensated Op-Amp Design

## Project Overview

This repository contains the design, theoretical calculations, and simulation files for a **Two-Stage Miller-Compensated Operational Amplifier**. The objective of this project was to design an Op-Amp driving a capacitive load while strictly adhering to given performance metrics, such as a high DC gain, specific common-mode range, and robust phase margin.

## Target Specifications

The constraints provided in the problem statement were:

* **DC Gain:** $\ge 2000$

* **Input Common Mode Range (ICMR):** 0.7 V to 1.6 V


* **Phase Margin:** $> 60^\circ$

* **Load Capacitance ($C_L$):** 5 pF


* **Gain-Bandwidth Product (GBW):** 50 MHz



## Methodology & Approach

The design process involved establishing the relationship between the required specifications and the physical parameters of the MOSFETs (Width and Length ratios).

1. **Mathematical Modeling:** Derived standard equations for Slew Rate, GBW, RHP Zero, and pole placement to ensure a dominant pole response.


2. **Scripting for Calculations:** We modeled the design equations in **Python** using NumPy to iteratively determine the exact $(W/L)$ ratios for all 8 transistors.


3. **Operating Conditions:** After iterating combinations, the final chosen configuration operates with $V_{DD} = 2.5V$, $V_{SS} = -1V$, Slew Rate ($SR$) $= 140 V/\mu s$, and Miller Compensation Capacitor ($C_c$) $= 6 pF$.



### Transistor Sizing (W/L Ratios)

Assuming a constant channel length of $L = 1\mu m$:

| Transistor | Type | W/L Ratio |
| --- | --- | --- |
| **M1, M2** | NMOS | 42.3 |
| **M3, M4** | PMOS | 46.67 |
| **M5, M8** | NMOS | 102.74 |
| **M6** | PMOS | 628.32 |
| **M7** | NMOS | 691.68 |

*Tail current ($I_5$) was calculated to be 840 $\mu A$.*
 

## Simulation Results

The circuit was constructed and verified using **LTSpice**. The simulation closely tracks the theoretical calculations across the common-mode voltage extremes ($0.7V$ and $1.6V$).

| Parameter | Target | Achieved ($V_{cm} = 0.7V$) | Achieved ($V_{cm} = 1.6V$) |
| --- | --- | --- | --- |
| **DC Gain** | 2000 | 2296 (67.22 dB) | 2143 (66.75 dB) |
| **GBW** | 50 MHz | 49.5 MHz | 49.3 MHz |
| **Phase Margin** | $> 60^\circ$ | $80.34^\circ$ | $80.38^\circ$ |

> *Conclusion: The design successfully achieved a single-pole system response over a wide frequency range, demonstrating excellent stability with a phase margin exceeding the target.*
> 

## Repository Structure

* `/docs` - Contains the original problem statement and our detailed mathematical report.


* `/scripts` - Python code used to iteratively solve the design equations for transistor sizing.


* `/simulations` - LTSpice `.asc` schematic files and `.raw` output data.



## Tools Used

* **LTSpice:** For AC, Transient, and DC Operating Point circuit simulations.


* **Python (NumPy):** For automating complex design equations.
