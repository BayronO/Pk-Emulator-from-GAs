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
- Calls **CLASS** to compute the linear transfer function.  
  Output: `Transfer_Function_h_omegab_omegam.txt`
- This file is used by `LCDM.nb`, where the GA-based symbolic regression is performed to obtain:
  - the smooth transfer function $T_{\mathrm{nw}}$,
  - the wiggle component \( T_{\mathrm{w}} \).

#### 1.2 Linear power spectra database
- Creates the directory `./Data/spectra_latin_hc/`. Contains all linear power spectra (spectrum_*.txt) used to test the emulator.

The corresponding cosmological parameters are stored in `cosmo_params.txt`

- Modifies the template `HaloFIT.ini` to compute the non-linear prediction of P(k) from class using halofit and store these spectra in `./Data/spectra_halofit/`
     1.4.  Store in `./Data/spectra_kmax/` the spectra required to find a fitting formula for $k_\max$ in `LCDM.nb`.

  2. LCDM.nb
     2.1.  The genetic algorithm code is implemented here.
     2.2.  Savitzky-Golay.ipynb creates the file Filtered_Tk.txt required to test the accuracy of the smoothed matter transfer function formulation in comparison with the expected accuracy obtained from the Savitzky-Golay filter.
     2.3.  pySR.ipynb implements a small routine in pySR to find a formula for the second derivative of the P(k) evaluated at $k_\max$.

  4. Modified_Gravity.nb
     Implements the parametric deformation of the LCDM spectrum in order to add typical effects due to modifications of gravity. Two study cases are exemplified: the f(R) Hu-Sawicki model, and the planck_late model.

  5. 2PTCorrelation.ipynb
     Routine to compute the 2-point correlation function using class and the Eisenstein-Hu formula for the smooth P(k), and our GAs base formulation for the smooth $P(k)$. We also compare the predictions from $\Lambda$CDM and the f(R) Hu-Sawicki model corresponding to the BAO scale, when using our parametric deformation for MG effects. 
        
 
