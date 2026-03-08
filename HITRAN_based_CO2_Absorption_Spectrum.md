# HITRAN-based CO₂ Absorption Spectrum Simulator

Author: **Arun Kumar Pandey**

This module implements a simplified **CO₂ absorption spectrum simulator**
based on spectroscopic parameters from the HITRAN database.  
It is designed as part of a **CO₂ Retrieval Simulator** used to study
how atmospheric carbon dioxide can be retrieved from spectroscopic
measurements.

The model computes the **absorption cross section** of CO₂ in the
**1.6 µm near-infrared band (~6200–6280 cm⁻¹)**, which is widely used
by satellite missions such as OCO-2 and GOSAT.

---

# Overview

The simulator performs the following steps:

1. Define spectroscopic line parameters
2. Apply temperature correction to line strengths
3. Compute spectral line broadening
4. Construct the spectral line profile
5. Sum all spectral lines to obtain the absorption cross section
6. Optionally download real HITRAN data using HAPI
7. Visualize spectra and concentration sensitivity

---

# Spectroscopic Background

Real molecular absorption lines are not infinitely narrow.
They are broadened by two main physical processes:

- **Doppler broadening (thermal motion)**
- **Pressure broadening (collisions)**

The resulting line shape in the atmosphere is the **Voigt profile**.

---

# Absorption Cross Section

The absorption cross section at wavenumber $ \nu $ is given by

$$
\sigma(\nu) = \sum_i S_i(T)\,\phi_i(\nu)
$$

where

- $ S_i(T) $ : line strength of transition $ i $
- $ \phi_i(\nu) $ : spectral line shape function

The simulator computes this for all lines in the spectral window.

---

# Line Strength Temperature Correction

HITRAN provides line strengths at a reference temperature

$$
T_{ref} = 296 \, K
$$

The line strength at temperature $T$ is

$$
S(T) =
S(T_{ref})
\frac{Q(T_{ref})}{Q(T)}
\exp\left[-\frac{hcE''}{k}\left(\frac{1}{T}-\frac{1}{T_{ref}}\right)\right]
\frac{1 - \exp(-hc\nu_0/kT)}
     {1 - \exp(-hc\nu_0/kT_{ref})}
$$

where

- $E''$ : lower state energy
- $Q(T)$ : partition function
- $h$ : Planck constant
- $k$ : Boltzmann constant
- $c$ : speed of light

In this simulator a simplified version is used.

---

# Spectral Line Broadening

## Doppler Broadening

Thermal motion of molecules produces a Gaussian profile

$$
\phi_D(\nu)
=
\frac{1}{\Delta\nu_D\sqrt{\pi}}
\exp\left(
-\frac{(\nu-\nu_0)^2}{\Delta\nu_D^2}
\right)
$$

The Doppler half-width is

$$
\Delta\nu_D
=
\frac{\nu_0}{c}
\sqrt{\frac{2k_B T \ln 2}{m}}
$$

where

- $T$ : temperature
- $m$ : molecular mass

---

## Pressure (Collisional) Broadening

Collisions between molecules produce a Lorentzian profile

$$
\phi_L(\nu)
=
\frac{\Delta\nu_L/\pi}
{(\nu-\nu_0)^2 + \Delta\nu_L^2}
$$

The Lorentzian half width scales with pressure:

$$
\Delta\nu_L
=
\gamma_{air}
\left(\frac{P}{P_{ref}}\right)^{n_{air}}
\left(\frac{T_{ref}}{T}\right)^{\delta}
$$

---

## Voigt Profile

In the real atmosphere both effects occur simultaneously.
The physical line shape is the convolution of the two:

$$
\phi_V(\nu)
=
\int_{-\infty}^{\infty}
\phi_D(\nu')
\phi_L(\nu-\nu')
d\nu'
$$

This convolution is evaluated numerically using the **Faddeeva function**.

---

# Synthetic CO₂ Line List

For offline operation the module includes a small synthetic
line list for the **CO₂ 1.6 µm band**.

Each line contains

| Parameter | Description |
|-----------|-------------|
| ν₀ | line center wavenumber |
| S | line strength |
| γ_air | air-broadened width |
| E'' | lower state energy |
| n_air | temperature exponent |

These values are **representative but not exact HITRAN data**.

---

# Optional HITRAN Integration

If the `hitran-api` package is installed the simulator can
download real spectroscopic data.

```sh
pip install hitran-api
````

Example:

```python
from hitran_model import download_hitran_co2

download_hitran_co2(6200, 6280)
````

This downloads CO₂ lines from the HITRAN database.

---

# Example Usage

```py
import numpy as np
from hitran_model import hitran_cross_section, SYNTHETIC_CO2_LINES

nu = np.linspace(6210, 6270, 5000)

pressure = 101325
temperature = 288

xsec = hitran_cross_section(
    nu,
    SYNTHETIC_CO2_LINES,
    pressure,
    temperature
)
```

---

# Visualization

The module includes plotting utilities:

### Plot absorption spectrum

```py
plot_hitran_spectrum(nu, xsec, SYNTHETIC_CO2_LINES)
```

### CO₂ sensitivity experiment

```py
plot_spectrum_sensitivity(
    nu,
    SYNTHETIC_CO2_LINES,
    co2_concentrations_ppm=[350,400,420,450,500]
)
```

This shows how atmospheric transmission changes with CO₂ concentration.

---

# Output

The simulator produces

* CO₂ absorption cross sections
* absorption spectra
* transmission curves
* concentration sensitivity plots

These outputs can be used for

* atmospheric radiative transfer studies
* satellite retrieval algorithm testing
* educational spectroscopy simulations

---

# Dependencies

```
numpy
matplotlib
hitran-api (optional)
```

---

# Scientific Applications

This model illustrates the physical basis of **satellite CO₂ retrieval algorithms** used in missions such as

* OCO-2
* GOSAT
* Sentinel-5P

It demonstrates how molecular spectroscopy translates into
observable absorption features used to estimate atmospheric
CO₂ concentrations.

---

# License

Educational / research use.

