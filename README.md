# Geostatistical MCMC Reconstruction of Jutulstraumen Subglacial Bed Topography
(final poster to be inserted)

This repository contains my final project for GLY4930 — Geophysical Exploration of the Cryosphere, where I apply a Markov chain Monte Carlo (MCMC) geostatistical framework to reconstruct high-resolution bed topography beneath the Jutulstraumen Glacier, East Antarctica.

The workflow adapts the methodology described in Shao et al. (in review), along with the companion codebase:
https://github.com/NiyaShao/geostatisticalMCMC

This README summarizes the glacier background, scientific motivation, method, workflow, and reproduction instructions.

## 🐧 Background: Jutulstraumen Glacier

Jutulstraumen is a major fast-flowing outlet glacier draining into the Fimbul Ice Shelf. It has the following features:

- A central trunk exceeding 400–500 m/yr

- Strong shear margins

- Deep, narrow subglacial troughs

- Sparse radar coverage along large portions of the flowline

Because the glacier funnels ice through a constrained basin, its modeled flow behavior and grounding-line stability depend sensitively on bed geometry. Accurate bed reconstruction is thus essential for realistic ice-flow modeling and understanding regional dynamics.

<figures to be inserted - index map, surface type, surface ice velocity>

## 🐧 Existing Bed Products: Limitations

BedMachine Antarctica v3

- Uses mass conservation + ice thickness + surface velocities

- Performs well where data are plentiful

- Smooths short-wavelength roughness in data-sparse regions

- May underestimate trough depth beneath fast-flowing trunks

BedMap3

- Continental-scale product

- Good for regional context

- Lower effective resolution

- Not tuned for outlet glacier subglacial detail

Both products struggle in Jutulstraumen because:

- Radar sounding lines are widely spaced

- Interpolation filters out important roughness

- Uncertainty is not quantified

- Sub-10-km features affecting basal drag are not recovered

<figures to be inserted - bedmap3 and bedmachine topographies>

## 🐧 Why Use MCMC + SGS?
Antarctic bed topography contains variations across many spatial scales:

- Large-scale (>10 km): basins, divides, regional troughs

- Intermediate scales: valley transitions, channel geometry

- Small-scale (<10 km): roughness influencing sliding

- Standard interpolation cannot recover this multi-scale structure, nor quantify uncertainty.

The MCMC + SGS method solves this by:

- [ ] Using MCMC to update the long-wavelength bed in a probabilistic framework

- [ ] Applying Sequential Gaussian Simulation (SGS) to regenerate high-frequency roughness

- [ ] Enforcing statistical consistency using fitted variogram models

- [ ] Producing ensembles of plausible bed surfaces

- [ ] Avoiding over-smoothing in regions lacking data

This approach is particularly useful for Jutulstraumen’s deep, narrow, fast-flowing trunk.

## 🐧 Method Overview

### Large-Scale MCMC Chain
The large-scale chain:

- Proposes long-wavelength bed surfaces

- Evaluates agreement with radar observations

- Uses a spatial covariance prior informed by variogram fitting

- Accepts or rejects proposals using MCMC rules

This produces a probabilistic ensemble of large-scale beds consistent with available data.

### Small-Scale SGS Reconstruction
SGS then:

- Subdivides the domain into smaller windows

- Replaces local roughness with SGS realizations

- Preserves variance, wavelength structures, and anisotropy

- Restores realistic roughness not captured by the MCMC stage

## Final Result 

(final image here)

## 🐧 Reproducibility Instructions

This project uses the same dependencies as the original implementation:
https://github.com/NiyaShao/geostatisticalMCMC

**Running the Workflow**

Run notebooks sequentially:

    T1_LoadData.ipynb

    T2_StatisticalAnalysis.ipynb

    T3_LargeScaleChain.ipynb

    T4_SmallScaleChain.ipynb

Ensure paths to BedMachine, MEaSUREs velocity, SMB, and dh/dt datasets are correct.
MCMC and SGS chains may require extended runtime depending on iteration count and resolution.

## 🐧 Citations 

**Method (Geostatistical MCMC + SGS)**

Shao, N., E. J. Mackie, M. J. Field, and F. S. McCormack.
"A Markov Chain Monte Carlo Approach for Geostatistically Simulating Mass-Conserving Subglacial Topography."
In review, *Journal of Glaciology.*

**Glacier Background & Flow Dynamics**

Rignot, E., et al. "Acceleration of Jutulstraumen Glacier, East Antarctica."
*Geophysical Research Letters* 38, 2011.

Moholdt, G., et al. "Mass change in East Antarctic outlet glaciers."
*Journal of Glaciology* 58(209), 2012.

**Bed Products & Mass Conservation**

Morlighem, M., et al. "Deep glacial troughs and stabilizing ridges unveiled beneath the margins of the Antarctic Ice Sheet."
*Nature Geoscience* 13, 132–137 (2020).

Fretwell, P., et al. (2023). "Bedmap3: A new Antarctic ice bed topography and thickness dataset." 
*The Cryosphere*, 17, 2169–2198.

**Variograms, Roughness, & Stochastic Simulation**

MacKie, E. J., et al. "Antarctic subglacial topography from multi-scale statistical inference."
*The Cryosphere* 14, 2351–2376 (2020).

**Data Usage**

All BedMachine, MEaSUREs velocity, SMB, and dh/dt datasets used in this project are sourced from NSIDC and processed locally.

## 🐧 Author
Apoorva Bangalore Raviprasad

University of Florida

GLY4930 — Geophysical Exploration of the Cryosphere

Fall 2025
