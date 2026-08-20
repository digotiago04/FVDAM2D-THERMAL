# 🔥 FVDAM-THERMAL

This repository features MATLAB codes developed to compute the effective thermal conductivity of periodic composite materials. The implementations include both a mean-field formulation and an energy-based formulation for numerical homogenization.

The models consider a square periodic unit cell containing a centered circular inclusion embedded in a surrounding matrix. Both the matrix phase and the inclusion (fiber) phase are assumed to be isotropic. In addition to evaluating the effective thermal conductivity matrix K<sup>*</sup>, the repository also provides visualization of the temperature field and microscopic temperature profiles along the coordinate directions.

---
## ⚙️ Features
* Highly vectorized, high-performance MATLAB implementation, minimizing loops and leveraging efficient sparse operations.
* Computes the effective thermal conductivity matrix K<sup>*</sup> from two unit macroscopic gradient tests.
* Periodic boundary conditions automatically enforced on the square RUC for thermal homogenization.
* Square periodic unit cell with a centered circular inclusion, where both matrix and inclusion are isotropic.
* Post-processing included: total temperature field visualization and microscopic temperature profiles along the coordinate directions.

<p align="center">
  <img src="imagens/RUC.png" width="600">
</p>

---

##  💻 Requirements
The implementation of this tool was entirely developed in the MATLAB environment (version R2022b). Its development did not require the use of additional tools or packages, so the code can be executed in a standard MATLAB installation.

---
## ▶️ Running the code
FVDAM is a numerical approach based on the spatial discretization of the RUC into subvolumes (finite volumes). To calculate the effective thermal conductivity  this repository offers **two distinct mathematical formulations:**

* **Based on Mean-Field Theory:** Mean-field theory is based on the principle that the effective thermal properties observed experimentally arise from averaging relationships between local fields (temperature gradients and heat fluxes) within microscopically heterogeneous materials. Consequently, the macroscopic fields are defined as volume averages of their corresponding microscopic fields, and the effective thermal properties emerge naturally from these average relations.

* **Based on Energy Theory:** In this approach, homogenization can be interpreted as the process of finding a homogeneous material that is energetically equivalent to a heterogeneous material with a complex microstructure. 


While these two theories take distinct mathematical routes, they are strictly equivalent. Both formulations lead to the exact same effective macroscopic properties, providing a double-validation of the numerical homogenization process.


### Syntax

The `FVDAMThermal_MF.m` and `FVDAMThermal_EB.m` functions compute the effective thermal conductivity matrix and plot the 2D temperature field for a composite material with a circular inclusion. Additionally, they extract the 1D micro-fields at specified cross-sections, directly comparing both the numerical profiles and the calculated effective conductivity against analytical results obtained from LEHT.
* FVDAMThermal_MF(ny1, ny2, k_m, k_i, frac, field, SVy1_cut, SVy2_cut)
* FVDAMThermal_EB(ny1, ny2, k_m, k_i, frac, field, SVy1_cut, SVy2_cut)

---
##  Inputs parameters declaration - FVDAM

Both functions share the following input arguments:

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `ny1` | `int` | Number of subvolumes along the $y_1$ direction. |
| `ny2` | `int` | Number of subvolumes along the $y_2$ direction. |
| `k_m` | `float` | Thermal conductivity of the matrix material $[\text{W}/(\text{m}\cdot\text{K})]$. |
| `k_i` | `float` | Thermal conductivity of the circular inclusion $[\text{W}/(\text{m}\cdot\text{K})]$. |
| `frac` | `float` | Inclusion volume fraction ($0 \le \text{frac} < 1$). |
| `field` | `int` | Flag to generate the 2D total temperature surface plot (`1` = active, `0` = disabled). |
| `SVy1_cut` | `int` | Subvolume index along $y_1$ to extract the vertical temperature profile. |
| `SVy2_cut` | `int` | Subvolume index along $y_2$ to extract the horizontal temperature profile. |

Markdown
### Usage Example

To run the thermal micromechanics analysis using an 80 × 80 subvolume mesh, a matrix thermal conductivity of 0.5 W/(m·K), an inclusion thermal conductivity of 4.5 W/(m·K), and a 60% inclusion volume fraction (`0.6`), while generating the 2D total temperature field surface and extracting temperature profiles at subvolumes 35 (along $y_1$) and 45 (along $y_2$), execute either of the following commands in the MATLAB Command Window:

```matlab

% Energy-Based Formulation
FVDAMThermal_EB(80, 80, 0.5, 4.5, 0.6, 1, 35, 45);

% Mean-Field Formulation
FVDAMThermal_MF(80, 80, 0.5, 4.5, 0.6, 1, 35, 45);

Plaintext
***Command Window Output:***

====================================================
EFFECTIVE THERMAL CONDUCTIVITY MATRICES (K*)
====================================================
FVDAM - ENERGY BASED 
    1.1824   -0.0000
   -0.0000    1.1824

====================================================
EFFECTIVE THERMAL CONDUCTIVITY MATRICES (K*)
====================================================
FVDAM - MEAN-FIELD 
    1.1824   -0.0000
   -0.0000    1.1824```

***Graphical Results:***

The command above will also generate the following plots:

|<img src="imagens/field_2dFVT.png" width="500"> | <img src="imagens/profile_xFVT.png" width="500"> | <img src="imagens/profile_yFVT.png" width="500"> |
| :---: | :---:  |:---: |
---


## ❌ Reporting issues

We strive to ensure that this Finite-Volume Theory implementation is accurate and efficient. However, if you encounter any unexpected behavior, inconsistencies, or potential bugs in the code, your feedback is highly appreciated.

Please feel free to reach out via email:
📩 diogo.santos@ctec.ufal.br

Your contributions help improve the reliability and usability of this project for the scientific community.

---

## 📚 Authors
Project developed by:
* Diogo Tiago dos Santos 📩 diogo.santos@ctec.ufal.br
* Márcio André Araújo Cavalcante 📩 marcio.cavalcante@ceca.ufal.br
* Romildo dos Santos Escarpini Filho 📩 romildo.escarpini@penedo.ufal.br
* Arnaldo dos Santos Júnior 📩 arnaldo@ctec.ufal.br
