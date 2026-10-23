# Discrete Hardware Realization of a Low-Cost Analog In-Memory Computing Core for Edge-Oriented Analog Classification

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23543959.svg)](https://doi.org/10.5281/zenodo.23543959)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![YouTube Demo](https://img.shields.io/badge/YouTube-Live%20Bench%20Demo-red?logo=youtube)](https://youtu.be/-FSi0YV9P7M)

**Lead Author & Hardware Architect:**  
**Md. Akram Sarker**  
- ¹ Department of Computer Science & Engineering, Varendra University, Rajshahi, Bangladesh  
- ² Department of Physics, National University, Bangladesh  
- Contact: `akram.com.bd@gmail.com`  
- Permanent Scientific DOI: [10.5281/zenodo.23543959](https://doi.org/10.5281/zenodo.23543959)

---

## 📌 Executive Abstract
Conventional digital computing architectures typically separate arithmetic computation and data storage, introducing notable latency and energy overhead due to continuous data movement. Analog In-Memory Computing (AIMC) offers an attractive paradigm by performing computational operations directly in the physical circuit domain using conductance-encoded weights. In this paper, we report a physical, low-cost discrete hardware realization of an analog computing core demonstrating conductance-weighted current summation and rail-limited binary output behavior. 

Weight values are represented by resistor-defined conductances according to Ohm’s Law ($I = V \cdot G$), while current summation is physically realized at an inverting junction governed by Kirchhoff’s Current Law. The prototype uses a commercially available Texas Instruments LM358 dual operational amplifier powered from a 9.72 V DC battery supply. Experimental bench measurements recorded an output of 9.55 V under the tested active-input condition and 0.00 V under the low-output condition, with a measured static supply current of 0.70 mA corresponding to 6.80 mW of measured quiescent supply power. The demonstrated hardware provides a low-cost, verifiable experimental platform for investigating conductance-based analog computation and its potential application to low-complexity edge biomedical signal processing.

---

## 🔬 Experimental Hardware Specifications & Measurements

| Parameter Name | Measured Value | Operational Meaning |
| :--- | :--- | :--- |
| **Operational Amplifier** | Texas Instruments LM358 (DIP-8) | Commercially available single-supply dual op-amp |
| **Supply Voltage ($V_{CC}$)** | **9.72 V DC** | Calibrated single DC battery supply rail |
| **Measured Quiescent Supply Current ($I_{CC}$)** | **0.70 mA** | Total measured quiescent supply current |
| **Measured Quiescent Supply Power ($P$)** | **6.80 mW** | $P = V_{CC} \times I_{CC} = 9.72\text{ V} \times 0.70\text{ mA} = 6.80\text{ mW}$ |
| **Measured Output under Active Input Condition** | **9.55 V** | Observed output voltage |
| **Measured Output under Low/Quiescent Condition** | **0.00 V** | Observed output voltage |
| **Input / Feedback Resistors ($R_{in}, R_f$)** | $10\text{ k}\Omega$ (1% Precision) | Nominal conductance $G = 100\ \mu\text{S}$ |

*Experimental Note:*  
An output voltage of 9.55 V was observed under the applied input condition. Further pin-level voltage measurements and circuit verification are required to establish whether the observed state represents intended classification behavior or single-supply operational-amplifier saturation dynamics.

---

## 📐 Mathematical Formulation & Circuit Principle

The computational core is described using a single-neuron weighted-summation model. For an input vector $X$, weight vector $W$, and bias term $b$, the neuron output can be expressed as:
$$Y = f\left(\sum_{i} X_i W_i + b\right)$$

In the physical analog circuit, computational weighting is represented by resistor-defined conductances.

### 1) Weight Encoding via Ohm’s Law
For an input voltage $V_i$ applied through an input resistance $R_i$, the corresponding conductance is:
$$G_i = \frac{1}{R_i}$$
The resulting branch current is:
$$I_i = V_i \cdot G_i = \frac{V_i}{R_i}$$
Thus, the resistor value determines the conductance-weighted contribution of each input.

### 2) Current Summation via Kirchhoff’s Current Law
All input currents converge at the inverting summing junction of the operational amplifier. According to Kirchhoff’s Current Law (KCL), the algebraic sum of currents at the junction is zero:
$$\sum_{i} I_i + I_f = 0$$
where $I_f$ is the feedback current. The accumulated input-current magnitude is therefore:
$$I_{sum} = \sum_{i} I_i = \sum_{i} \frac{V_i}{R_i}$$

### 3) Linear Analog Summation
For an ideal inverting summing configuration with feedback resistance $R_f$, the corresponding linear output relation is:
$$V_{out} = -R_f \sum_{i} \frac{V_i}{R_i}$$
The negative sign denotes the inverting polarity of the operational-amplifier configuration.

### Numerical Verification Example (Two-Input Weighted Summation)
Consider two input branches with:
* $V_1 = 1.0\text{ V}, \quad R_1 = 10\text{ k}\Omega$
* $V_2 = 0.5\text{ V}, \quad R_2 = 20\text{ k}\Omega$

The corresponding branch currents are:
$$I_1 = \frac{1.0\text{ V}}{10\text{ k}\Omega} = 100\ \mu\text{A}$$
$$I_2 = \frac{0.5\text{ V}}{20\text{ k}\Omega} = 25\ \mu\text{A}$$

Therefore, the accumulated input current is:
$$I_{sum} = I_1 + I_2 = 125\ \mu\text{A}$$

For a feedback resistance of $R_f = 10\text{ k}\Omega$, the ideal linear output magnitude is:
$$|V_{out}| = I_{sum} R_f = (125\ \mu\text{A})(10\text{ k}\Omega) = 1.25\text{ V} \quad (\text{ideal signed } V_{out} = -1.25\text{ V})$$

*This calculated value represents the ideal linear weighted-summation response of the inverting stage. It should not be interpreted as the experimentally measured binary high-state output. The experimentally observed output states of 9.55 V and 0.00 V are reported separately in Section IV and must be interpreted from the complete implemented circuit topology and its operating conditions.*

---

## 🎥 Verified Demonstration Video
The experimental test bench setup and live voltage measurements can be viewed on YouTube:  
▶️ **[https://youtu.be/-FSi0YV9P7M](https://youtu.be/-FSi0YV9P7M)**

---

## 🦾 Prospective Biomedical Application & Discussion
In future prosthetic interface research, an appropriately filtered and conditioned surface Electromyography (sEMG) bio-potential envelope could be applied to this analog core, allowing appropriately conditioned signal excursions to generate low-latency binary control signals for robotic prosthetic actuation without requiring digital microcontroller overhead.

---

## 📖 How to Cite This Research
```bibtex
@misc{sarker2026discrete,
  author       = {Md. Akram Sarker},
  title        = {Discrete Hardware Realization of a Low-Cost Analog In-Memory Computing Core for Edge-Oriented Analog Classification},
  year         = {2026},
  publisher    = {Zenodo},
  doi          = {10.5281/zenodo.23543959},
  url          = {https://doi.org/10.5281/zenodo.23543959}
}
