# FinAP2ReBAP

FinAP2ReBAP is a MATLAB implementation for reconstructing brachial artery pressure (BAP) from noninvasive finger pressure measurements. This project attempts to replicate the algorithms used in the Finometer Model 1 [1] correcting for pulse wave distortions and pressure gradients. Two level-shifting implementations are included:

1. **Default implementation**
2. **Return-to-Flow (RTF) implementation**, leveraging the methodology described in the referenced papers. The input of the function is either:

   ```matlab
   ReBAP = FinAP2ReBAP(t, FinAP) % default
   ```

   or

   ```matlab
   ReBAP = FinAP2ReBAP(t, FinAP, PcuffRTF)
   ```

---

## Key Features

- **Pulse wave distortion correction** using a frequency-dependent filter.
- **Accurate pressure gradient correction** methods.
- Support for **customizable level-shifting strategies**.

---

## Core Equations

### Pulse Wave Distortion Correction

```math
H(f) = K \cdot \frac{(1 + i f / f_0)^2}{1 + 2i D f / f_1 - (f / f_1)^2}
```

Where:
- $$H(f)$$: Transfer function.
- $$K = 0.84$$: Gain. [2]
- $$f_1 = 7.34$$: Resonance frequency. [2]
- $$f_0 = f_1 \sqrt{K}$$: Aperiodic high-emphasis frequency. [2]
- $$D = 0.36$$: Damping coefficient.  [2]

```math
FinAP_\text{filtered}(t) = FinAP(t) \ast h(t)
```

### Level Correction

```math
ReBAP = FinAP_\text{filtered} - \Delta P 
```

#### Default Regression-Based Implementation [2]

```math
\Delta P = -13.3 - 0.194 \cdot P_\text{sys} + 0.574 \cdot P_\text{dias}
```

Where:


-  $$P_\text{sys}$$: Inverse-modeled finger systolic pressure, derived as:
  
  ```math
  P_\text{sys} = \text{Sys}(\text{FinAP}_\text{filtered}(t))
  ```

- $$P_\text{dias}$$: Inverse-modeled finger diastolic pressure, derived as:
  
  ```math
  P_\text{dias} = \text{DiaSys}(\text{FinAP}_\text{filtered}(t))
  ```

#### Return-to-Flow (RTF) Implementation [3]



and

```math
\text{Corr} = 18.7 + 0.44 \cdot P_\text{cuff RTF} - 0.36 \cdot FP_\text{sys} - 0.34 \cdot FP_\text{dias}
```

Where:
- $$FP_\text{corrected}$$: Corrected finger pressure.
- $$FP_\text{uncorrected}$$: Uncorrected finger pressure.
- $$P_\text{cuff RTF}$$: Return-to-Flow cuff pressure.
- $$FP_\text{sys}$$: Systolic finger pressure.
- $$FP_\text{dias}$$: Diastolic finger pressure.

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
1. Wesseling, K. H. (2002). Finometer User's Guide: Model 1.

2. Gizdulich, P., Prentza, A., & Wesseling, K.H. (1997). Models of brachial to finger pulse wave distortion and pressure decrement. *Cardiovascular Research, 33*(3), 698-705. [DOI:10.1016/S0008-6363(97)00003-5](https://doi.org/10.1016/S0008-6363(97)00003-5).
   
3. Bos, W.J.W., van Goudoever, J., van Montfrans, G.A., van den Meiracker, A.H., & Wesseling, K.H. (1996). Reconstruction of Brachial Artery Pressure From Noninvasive Finger Pressure Measurements. *Circulation, 94*(8), 1870-1875. [DOI:10.1161/01.CIR.94.8.1870](https://doi.org/10.1161/01.CIR.94.8.1870).


---

## License

This project is released under the MIT License. See the [LICENSE](LICENSE) file for more details.

---

## Contact

For questions or support, please open an issue or contact the repository maintainer.

---
