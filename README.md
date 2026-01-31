# Selected SDSS Spectrometry

This repository contains a Jupyter Notebook that performs spectral analysis on a selected set of extragalactic objects from the Sloan Digital Sky Survey (SDSS). The sample consists primarily of galaxies and quasars in the region surrounding the quasar 3C 273.

For each object, the notebook plots wavelength versus flux with prominent emission and absorption features annotated. Selected features are fit with Gaussian profiles to estimate redshifts, which are then used to construct a Hubble diagram for the sample.

The workflow is linear and notebook-driven, with intermediate plots intended to be inspected directly as part of the analysis.


## Overview

The analysis proceeds roughly as follows:
* Load SDSS FITS spectra and associated metadata
* Load a reference table of known spectral features
* Plot individual spectra with annotated emission and absorption lines
* Select prominent features for analysis
* Fit Gaussian profiles to those features
* Compute redshifts from fitted line centers
* Use the resulting redshifts to construct a Hubble diagram

The focus is on tracing how redshift estimates arise from individual spectral features rather than on automated classification.


## Spectrum visualization

Each object’s spectrum is plotted in observed wavelength, with a secondary axis showing rest-frame wavelength after correcting for redshift. Emission and absorption features are marked with dashed vertical lines and labeled by species.

Line selection depends on object classification: galaxies use both emission and absorption features, while quasars use emission lines only. Label placement and opacity are adjusted to remain legible in regions with many overlapping features.

### Example spectra

Broadline quasar:

<img src="sample_plots/broad-line quasar spectrum.png" width="640">

Corresponding Gaussian fit for a selected emission feature:

<img src="sample_plots/broad-line quasar line fit.png" width="480">

<br>

Starburst galaxy:

<img src="sample_plots/starburst galaxy spectrum.png" width="640">

Corresponding Gaussian fit for a narrow emission line:

<img src="sample_plots/starburst galaxy line fit.png" width="480">

<br>

Typical galaxy:

<img src="sample_plots/low-z galaxy spectrum.png" width="620">


## Line fitting and redshift calculation

A predefined set of prominent spectral features is selected for analysis. For each feature, the notebook extracts a local wavelength window and fits a Gaussian profile plus baseline.

From the fitted center wavelength and the known rest wavelength of the feature, an observed redshift is calculated. Uncertainties from the fit are propagated through subsequent velocity and distance calculations.

The Gaussian fit plots show the fitted curve overlaid on the local spectrum, along with the estimated mean wavelength, uncertainty, and full width at half maximum.


## Hubble diagram

Using the fitted redshifts, the notebook computes relativistic recessional velocities and estimates distances via Hubble’s law. These values are plotted in a two-panel Hubble diagram.

<img src="sample_plots/hubble diagram.png" width="500">

The top panel shows radial velocity versus distance on a logarithmic scale, with a reference line indicating the speed of light.
The bottom panel shows redshift versus distance on a linear scale.


## Data requirements

Running the notebook requires SDSS data in the same format used here:
* FITS spectra files containing wavelength, flux, and model data
* A CSV table of SDSS object metadata (coordinates, classifications, redshifts)
* A CSV list of reference spectral features with rest wavelengths and weights

The pipeline assumes SDSS-style FITS structures and metadata fields. While the analysis should generalize to other SDSS spectra with the same format, it was developed and tested on this specific selection.
