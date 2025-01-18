# FinAP2ReBAP

FinAP2ReBAP is a MATLAB implementation for reconstructing brachial artery pressure (BAP) from noninvasive finger pressure measurements. This project employs advanced modeling techniques to correct for pulse wave distortions and pressure gradients. Two level-shifting implementations are included:

1. **Default implementation**
2. **Return-to-Flow (RTF) implementation**, leveraging the methodology described in the referenced papers.

---

## Key Features

- **Pulse wave distortion correction** using a frequency-dependent filter.
- **Accurate pressure gradient correction** methods.
- Support for **customizable level-shifting strategies**.

---

## Core Equations

### Pulse Wave Distortion Correction

```math
H(f) = K \cdot \frac{(1 + j f / f_d)}{1 + 2j \xi f / f_r - (f / f_r)^2}
```

Where:
- \(H(f)\): Transfer function.
- \(K\): Gain.
- \(f_d\): Aperiodic high-emphasis frequency.
- \(f_r\): Resonance frequency.
- \(\xi\): Damping coefficient.

### Level Correction (Regression-Based)

```math
\Delta P = -13.3 - 0.194 \cdot P_\text{sys} + 0.574 \cdot P_\text{dias}
```

Where:
- \(P_\text{sys}\): Systolic pressure.
- \(P_\text{dias}\): Diastolic pressure.

---

## Usage

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/FinAP2ReBAP.git
   ```

2. Ensure MATLAB and required toolboxes are installed.

3. Load your data and configure input parameters.

4. Run the script:
   ```matlab
   FinAP2ReBAP
   ```

---

## Default vs. RTF Implementation

- **Default Implementation**: Applies generalized corrections.
- **RTF Implementation**: Incorporates Return-to-Flow measurements for increased accuracy, particularly in cases with significant pulse wave distortions.

---

## References

This work is based on methodologies and findings from the following papers:

1. Bos, W.J.W., van Goudoever, J., van Montfrans, G.A., van den Meiracker, A.H., & Wesseling, K.H. (1996). Reconstruction of Brachial Artery Pressure From Noninvasive Finger Pressure Measurements. *Circulation, 94*(8), 1870-1875. [DOI:10.1161/01.CIR.94.8.1870](https://doi.org/10.1161/01.CIR.94.8.1870).

2. Gizdulich, P., Prentza, A., & Wesseling, K.H. (1997). Models of brachial to finger pulse wave distortion and pressure decrement. *Cardiovascular Research, 33*(3), 698-705. [DOI:10.1016/S0008-6363(97)00003-5](https://doi.org/10.1016/S0008-6363(97)00003-5).

---

## License

This project is released under the MIT License. See the [LICENSE](LICENSE) file for more details.

---

## Contact

For questions or support, please open an issue or contact the repository maintainer.

---
