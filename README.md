# P(k) Emulator via Genetic Algorithms

This repository presents a **semi-analytical emulator for the linear matter power spectrum**, constructed using **Genetic Algorithms (GAs) for symbolic regression**.  
The emulator provides an interpretable and physically motivated representation of the matter transfer function and power spectrum, with accuracy comparable to standard numerical approaches.

A lightweight **tutorial (implemented in *Mathematica*)** is included, demonstrating the full methodology and several concrete examples.  
All results can be independently reproduced using the codes provided in this repository.

---

## Project Structure and Methodology

The workflow is organized as follows:

---

### 1. `Data_LCDM.nb`

This notebook generates the reference datasets required to train and validate the emulator.

#### 1.1 Transfer function generation
- Calls CLASS to compute the linear transfer function.  
  Output: `Transfer_Function_h_omegab_omegam.txt`
- This file is used by `LCDM.nb`, where the GA-based symbolic regression is performed to obtain:
  - the smooth transfer function $T_{\mathrm{nw}}$,
  - the wiggle component $T_{\mathrm{w}}$.

#### 1.2 Linear power spectra database
- Creates the directory `./Data/spectra_latin_hc/`. Contains all linear power spectra (`spectrum_*.txt`) used to test the emulator.
- The corresponding cosmological parameters are stored in `cosmo_params.txt`

#### 1.3 Non-linear spectra
- Automatically modifies the template `HaloFIT.ini` to compute the non-linear matter power spectrum using **CLASS $+$ HALOFIT**. Outputs are stored in `./Data/spectra_halofit/`.

### 1.4 $k_\max$
- Stores in `./Data/spectra_kmax/` the spectra required to derive a fitting formula for the characteristic scale $k_\max$​, later analyzed in `LCDM.nb`.

### 2. LCDM.nb
This notebook contains the core implementation of the Genetic Algorithm and the symbolic emulator construction.

### 2.1 Genetic Algorithm implementation
- Symbolic regression is used to infer compact and interpretable expressions for the smooth and oscillatory components of the matter transfer function.

### 2.2 Smoothing validation
- `Savitzky-Golay.ipynb` generates `Filtered_Tk.txt`. This file is used to assess the accuracy of the analytical smoothing procedure by comparison with a standard Savitzky–Golay filter.

### 2.3 Auxiliary symbolic regression with PySR
- `pySR.ipynb` implements a minimal **PySR** routine to obtain an analytical expression for the second derivative of $P(k)$ evaluated at $k_\max$.

### 3. `Modified_Gravity.nb`
This notebook introduces parametric deformations of the $\Lambda\mathrm{CDM}$ power spectrum to incorporate typical signatures of modified gravity (MG) theories. Two representative case studies are provided: Hu–Sawicki $f(R)$ gravity, planck_late modified gravity model.

These examples illustrate how the GA-based emulator can be systematically extended beyond standard $\Lambda\mathrm{CDM}$.

### 4. `2PTCorrelation.ipynb`
This notebook computes the two-point correlation function (2PCF) and analyzes BAO-scale observables.

The 2PCF is computed using **CLASS**, the **Eisenstein–Hu smooth power spectrum**, and the GA-based smooth $P(k)$ developed in this work.

We compare:
- $\Lambda\mathrm{CDM}$ vs. Hu–Sawicki $f(R)$ predictions,
- the impact of MG-induced deformations on the BAO scale.

## Reproducibility

All figures, fits, and numerical results presented in this repository can be fully reproduced using the provided notebooks and scripts, assuming a working installation of CLASS, Mathematica, and the Python dependencies listed in the notebooks.

## Citation
If you use this code, the emulator, or any part of this repository in your research, please cite the following papers:
- "Fully Interpretable Emulator for the Linear Matter Power Spectrum from Physics-Informed Machine Learning" https://arxiv.org/abs/2407.16640 
- "Machine learning unveils the linear matter power spectrum of modified gravity" https://arxiv.org/abs/2307.03643
- "Using machine learning to compress the matter transfer function $T(k)$" https://arxiv.org/abs/2211.06393
- Symbolic regression is used to infer compact and interpretable expressions for the smooth and oscillatory components of the matter transfer function.
   
  
