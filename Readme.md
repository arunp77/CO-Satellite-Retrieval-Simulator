# CO₂ Satellite Retrieval Simulator

A Python-based scientific project that demonstrates the fundamental physics behind **satellite measurements of atmospheric CO₂**. The project implements simplified models of **radiative transfer, molecular absorption, and satellite forward modeling**, which are the core components used in modern greenhouse gas monitoring missions.

This project was developed as an **independent technical study of satellite CO₂ retrieval algorithms** used in missions such as **OCO-2, MicroCarb, Sentinel-5P, and GOSAT**.

---

# Project Motivation

Satellite instruments measure atmospheric gases by observing how sunlight is absorbed by molecules in the atmosphere. Carbon dioxide has distinct absorption features in the **shortwave infrared (SWIR)** spectral region. By analyzing these absorption features, retrieval algorithms estimate the atmospheric CO₂ concentration.

The physical basis of these measurements is governed by the **radiative transfer equation** and **Beer–Lambert absorption law**.

Radiative transfer equation:

$$
\frac{dI_\nu}{ds} = -\kappa_\nu I_\nu + j_\nu
$$

Beer–Lambert absorption law:

$$
I_\nu = I_{\nu,0} e^{-\tau_\nu}
$$

where

* $I_\nu$ : observed radiance
* $I_{\nu,0}$ : incident solar radiance
* $\tau_\nu$ : optical depth

The optical depth depends on gas absorption:

$$
\tau_\nu = \sigma_\nu n L
$$

where

* $ \sigma_\nu $ : molecular absorption cross section
* $ n $ : gas number density
* $ L $ : photon path length

This project reproduces these physical processes using Python simulations.

---

# Project Objectives

The main objective of this project is to simulate the basic components of satellite CO₂ measurements:

1. Beer–Lambert absorption modeling
2. CO₂ spectral absorption lines
3. Simplified radiative transfer forward model
4. Satellite radiance simulation

The project provides an educational demonstration of how **spectroscopic absorption leads to observable spectral signatures in satellite measurements**.

---

# Repository Structure

```
co2_retrieval_simulator

├── notebooks
│   ├── 01_beer_lambert.ipynb
│   ├── 02_co2_spectral_line.ipynb
│   └── 03_forward_model.ipynb
│
├── src
│   ├── absorption.py
│   ├── spectroscopy.py
│   └── radiative_transfer.py
│
├── figures
│
├── README.md
```

---

# Simulation Components

## 1 Beer–Lambert Absorption

This module demonstrates how radiation intensity decreases when passing through a gas.

$$
I = I_0 e^{-\sigma n L}
$$

where

* $I_0$ : incoming radiation
* $I$ : transmitted radiation

This process explains how atmospheric gases imprint spectral signatures in satellite observations.

---

## 2 CO₂ Spectral Line Simulation

CO₂ absorbs radiation at specific wavelengths corresponding to molecular transitions. A simplified Gaussian line profile is used to model the absorption feature.

$$
\sigma(\nu) =
\sigma_0 \exp
\left(
-\frac{(\nu - \nu_0)^2}{2\sigma_\nu^2}
\right)
$$

This represents the molecular absorption feature measured by satellite spectrometers.

---

## 3 Radiative Transfer Forward Model

Satellite instruments measure radiance after atmospheric absorption:

$$
I(\nu) = I_0(\nu) e^{-\tau(\nu)}
$$

The forward model computes the observed spectrum after CO₂ absorption along the atmospheric path.

---

# Example Output

The simulations generate several physically meaningful outputs:

* exponential absorption curves
* CO₂ spectral absorption features
* synthetic satellite radiance spectra

These outputs illustrate how atmospheric CO₂ affects measured radiation.

---

# Scientific Background

The project is based on fundamental concepts used in satellite retrieval algorithms:

* Radiative transfer theory
* Atmospheric spectroscopy
* Molecular absorption physics
* Satellite forward modeling

These principles form the basis of operational greenhouse gas retrieval systems used in modern Earth observation missions.

---

# Possible Extensions

This simulator can be extended to include more realistic physics:

* HITRAN spectroscopic line databases
* Voigt line profiles (Doppler + pressure broadening)
* multilayer atmospheric models
* scattering from aerosols and clouds
* retrieval algorithms for XCO₂ estimation

These additions would move the project closer to real satellite retrieval systems.

---

# Tools and Libraries

The project uses:

* Python
* NumPy
* Matplotlib
* Jupyter Notebook


---

# License

This project is intended for educational and scientific purposes.


---

# CO₂ Satellite Retrieval Simulator

A Python-based scientific project that demonstrates the fundamental physics behind **satellite measurements of atmospheric carbon dioxide (CO₂)**. The project implements simplified models of **radiative transfer, molecular spectroscopy, and forward radiance modeling**, which form the foundation of modern satellite greenhouse gas retrieval algorithms.

This project was developed as an **independent technical study of CO₂ retrieval techniques used in Earth observation missions** such as:

* OCO-2 (NASA)
* MicroCarb (CNES / UKSA)
* GOSAT (JAXA)
* Sentinel-5P (ESA)

The objective is to reproduce, in simplified form, the physical processes that allow satellites to measure atmospheric CO₂ from space.

---

# Scientific Background

Satellite instruments measure atmospheric CO₂ by observing how sunlight is absorbed as it travels through the atmosphere. The observed spectrum contains **absorption features** caused by CO₂ molecules.

The physical foundation of these measurements is described by the **radiative transfer equation**:

[
\frac{dI_\nu}{ds} = -\kappa_\nu I_\nu + j_\nu
]

where

* (I_\nu) : spectral radiance
* (\kappa_\nu) : absorption coefficient
* (j_\nu) : emission term

For solar backscatter measurements in the shortwave infrared, emission can often be neglected, giving the **Beer–Lambert law**:

[
I_\nu = I_{\nu,0} e^{-\tau_\nu}
]

The optical depth is defined as

[
\tau_\nu = \int \sigma_\nu n(s) ds
]

where

* ( \sigma_\nu ) : molecular absorption cross section
* ( n(s) ) : gas number density
* ( ds ) : photon path element

This relationship forms the basis of satellite CO₂ retrieval algorithms.

---

# Project Objectives

This project aims to simulate the core physical components of satellite CO₂ measurements:

1. Beer–Lambert absorption modeling
2. CO₂ spectral absorption lines
3. Radiative transfer forward modeling
4. Synthetic satellite radiance simulation
5. Conceptual XCO₂ retrieval

The project provides an educational demonstration of how **atmospheric spectroscopy leads to measurable spectral signatures in satellite observations**.

---

# Repository Structure

```
co2_retrieval_simulator

├── notebooks
│   ├── 01_beer_lambert.ipynb
│   ├── 02_co2_spectral_line.ipynb
│   ├── 03_forward_model.ipynb
│   └── 04_xco2_retrieval.ipynb
│
├── src
│   ├── absorption.py
│   ├── spectroscopy.py
│   ├── radiative_transfer.py
│   └── retrieval.py
│
├── figures
│
├── data
│   └── hitran_lines.txt
│
└── README.md
```

---

# Simulation Components

## Beer–Lambert Absorption

The Beer–Lambert law describes how radiation intensity decreases when passing through an absorbing medium:

[
I = I_0 e^{-\sigma n L}
]

where

* (I_0) : incident radiation
* (I) : transmitted radiation
* ( \sigma ) : absorption cross section
* ( n ) : molecular number density
* ( L ) : photon path length

This process explains how atmospheric gases create spectral absorption signatures.

---

# CO₂ Spectral Absorption

CO₂ absorbs radiation at discrete spectral lines corresponding to molecular transitions.

The project simulates simplified spectral features using Gaussian or Voigt line profiles.

Gaussian line profile:

[
\sigma(\nu) =
\sigma_0
\exp
\left(
-\frac{(\nu - \nu_0)^2}{2\sigma^2}
\right)
]

Real atmospheric spectroscopy requires **Voigt profiles**, which combine Doppler and pressure broadening effects.

---

# Voigt Line Profile

The Voigt function combines two physical broadening mechanisms:

Doppler broadening (thermal motion):

[
\phi_D(\nu)
]

Pressure broadening (collisions):

[
\phi_L(\nu)
]

The resulting Voigt profile is

[
\phi_V(\nu) =
\int
\phi_D(\nu') \phi_L(\nu - \nu') d\nu'
]

This is the standard spectral model used in atmospheric spectroscopy.

---

# HITRAN Spectroscopic Database

Real satellite retrieval algorithms rely on the **HITRAN molecular spectroscopy database**, which provides:

* molecular line positions
* line strengths
* pressure broadening coefficients
* temperature dependence parameters

The project can be extended to load HITRAN line parameters and simulate realistic CO₂ absorption spectra.

---

# Forward Radiative Transfer Model

Satellite instruments measure radiance after atmospheric absorption:

[
I(\nu) = I_0(\nu) e^{-\tau(\nu)}
]

where

[
\tau(\nu) = \sum_i \sigma_i(\nu) n_i L_i
]

The forward model computes the radiance spectrum that would be observed by a satellite spectrometer.

---

# Atmospheric Layer Model

The atmosphere can be divided into multiple layers:

[
\tau(\nu) =
\sum_{layers}
\sigma(\nu) n_i L_i
]

Each layer contributes to the total optical depth depending on its pressure, temperature, and CO₂ concentration.

---

# XCO₂ Retrieval Concept

Satellite missions retrieve the **column-averaged dry-air mole fraction of CO₂**, known as XCO₂.

[
XCO_2 =
\frac{\int n_{CO_2}(z) dz}{\int n_{dry,air}(z) dz}
]

Retrieval algorithms estimate XCO₂ by fitting simulated spectra to measured radiance using optimization techniques.

---

# Example Outputs

The simulations generate:

* Beer–Lambert absorption curves
* synthetic CO₂ spectral lines
* simulated satellite radiance spectra
* simplified retrieval demonstrations

These outputs illustrate how atmospheric CO₂ affects satellite observations.

---

# Tools and Libraries

The project uses

* Python
* NumPy
* SciPy
* Matplotlib
* Jupyter Notebook

---

# Possible Extensions

Future improvements may include:

* full HITRAN spectroscopy integration
* multilayer atmospheric radiative transfer
* aerosol scattering models
* optimal estimation retrieval algorithms
* comparison with real satellite spectra

---

# Author

Arun Kumar Pandey
Remote sensing scientist and data engineer working on Earth observation systems.

GitHub
[https://github.com/arunp77](https://github.com/arunp77)

---

# License

This project is intended for educational and scientific purposes.

---

## If you want, the **next step I recommend** is extremely interesting scientifically.

We can implement a **real CO₂ spectrum using HITRAN data (just like OCO-2 retrieval algorithms)**.

That would make this project look **very close to an actual satellite retrieval model** and would be **very impressive in your portfolio**.

