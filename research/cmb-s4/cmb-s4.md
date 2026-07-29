---
layout: inner
title: "Forecasting Constraints on Primordial Gravitational Waves"
permalink: /research/cmb-s4/
---

# Forecasting Constraints on Primordial Gravitational Waves

*Using CMB-S4 B-mode polarization forecasts to study scale-dependent primordial tensor perturbations.*

**Institution:** University of Washington  
**Department:** Department of Physics  
**Research period:** March 2022–June 2023  
**Advisor:** Prof. Marilena LoVerde  
**Collaborator:** Zach Weiner  
**Presentation:** 241st Meeting of the American Astronomical Society, Seattle, January 2023

<a class="btn btn-default btn-lg"
   href="https://aas241-aas.ipostersessions.com/Default.aspx?s=73-8F-44-9D-6A-D0-58-4A-2F-96-42-B6-AF-88-A7-15"
   target="_blank"
   rel="noopener noreferrer">
  <i class="fa fa-external-link"></i> View the Interactive Poster
</a>

---

## Project Overview

This project investigated how future measurements of cosmic microwave background polarization could constrain **primordial gravitational waves** across a broad range of physical scales.

Most forecasts for inflationary gravitational waves assume a nearly scale-invariant primordial tensor power spectrum described by a single tensor-to-scalar ratio, \(r\). However, primordial gravitational waves may also be generated through other early-universe processes, including phase transitions, and may therefore have a nontrivial scale-dependent spectrum.

I developed a Python forecasting pipeline that used the public Boltzmann code **CLASS** to propagate a general primordial tensor power spectrum into an observable CMB B-mode polarization spectrum. I then used a Fisher-matrix analysis to estimate how well CMB-S4 could constrain the amplitude of primordial tensor perturbations in separate wavenumber bins.

![CMB-S4 research poster]({{ '/research/cmb-s4/cmb-s4-poster.pdf' | relative_url }})

*Interactive research poster presented at the 241st Meeting of the American Astronomical Society.*

---

## The Cosmic Microwave Background

The **cosmic microwave background**, or CMB, is relic radiation from the early universe.

Before recombination, photons, electrons, and atomic nuclei formed a tightly coupled photon–baryon plasma. As the universe expanded and cooled, electrons combined with nuclei to form neutral atoms approximately 380,000 years after the Big Bang. Photons were then able to travel largely without repeated scattering.

Those photons form the CMB observed today.

Small primordial perturbations produced acoustic waves in the early plasma. Overdense regions were compressed and heated, while underdense regions became comparatively rarefied and cooler. When photons decoupled from matter, these variations were preserved as the temperature anisotropies visible in CMB maps.

![Cosmic microwave background temperature anisotropies]({{ '/research/cmb-s4/cmb-map.jpg' | relative_url }})

*Temperature anisotropies in the cosmic microwave background. The temperature variations are extremely small compared with the mean CMB temperature.*

The angular structure of the CMB is commonly described using spherical harmonics and the multipole number \(\ell\). Low multipoles correspond to large angular scales on the sky, while high multipoles correspond to smaller angular scales.

---

## Primordial Perturbations and Gravitational Waves

Inflation proposes that the early universe underwent a period of accelerated expansion. Quantum fluctuations generated during this era may have been stretched to cosmological scales and become the initial perturbations from which later structure developed.

These primordial perturbations can be separated into two principal components:

- **Scalar perturbations**, associated with density variations
- **Tensor perturbations**, associated with primordial gravitational waves

Primordial gravitational waves are tensor perturbations of spacetime. If they were generated during inflation or another early-universe process, they could leave a characteristic imprint on the polarization of the CMB.

![Illustration of gravitational waves]({{ '/research/cmb-s4/primordial-gravitational-waves.jpg' | relative_url }})

*Illustration of gravitational waves propagating through spacetime.*

---

## Tensor-to-Scalar Ratio

For a simple inflationary model, the primordial tensor power spectrum may be written as

\[
P_t(k)=A_t\left(\frac{k}{k_p}\right)^{n_t},
\]

where:

- \(A_t\) is the primordial tensor amplitude,
- \(k_p\) is the pivot wavenumber,
- \(n_t\) is the tensor spectral index.

The tensor-to-scalar ratio is

\[
r=\frac{A_t}{A_s},
\]

where \(A_s\) is the primordial scalar amplitude.

For an approximately scale-invariant tensor spectrum, \(n_t\) is close to zero. Under inflationary assumptions, a constraint on \(r\) also constrains the amplitude of tensor perturbations and the characteristic energy scale associated with inflation.

---

## CMB Polarization and B Modes

CMB polarization can be decomposed into two geometrically distinct patterns:

- **E-mode polarization**
- **B-mode polarization**

Scalar density perturbations generate E-mode polarization but do not directly produce primordial B modes at linear order. Tensor perturbations can produce both E and B modes.

A primordial B-mode signal could therefore provide evidence for primordial gravitational waves. However, gravitational lensing also converts part of the scalar-generated E-mode signal into B-mode polarization. Galactic foregrounds and instrumental noise provide additional sources of contamination.

The observed B-mode power spectrum must therefore be modeled as a combination of:

- Primordial tensor B modes
- Lensing-induced B modes
- Foreground emission
- Instrumental noise

![Example CMB temperature and polarization power spectra]({{ '/research/cmb-s4/cmb-polarization-spectra.jpg' | relative_url }})

*Example temperature, E-mode, and B-mode angular power spectra.*

---

## A Scale-Dependent Tensor Power Spectrum

Rather than assuming that the complete tensor spectrum could be described by one value of \(r\), I modeled a general scale-dependent spectrum over a broad range of Fourier wavenumbers.

The range

\[
10^{-6}\ {\rm Mpc}^{-1} \lesssim k \lesssim 10\ {\rm Mpc}^{-1}
\]

was divided into 15 logarithmically spaced bins.

The spectrum was represented schematically as

\[
P_t(k)=\sum_i p_i W_i(k),
\]

where \(p_i\) is the tensor amplitude in bin \(i\), and \(W_i(k)\) is a smooth window function.

To avoid discontinuous bin boundaries, the windows were constructed using complementary error functions. A normalized smooth top-hat window can be written as

\[
W_i(k)=\frac{1}{2}
\left[
\operatorname{erfc}
\left(
\frac{\ln k_{i,\mathrm{left}}-\ln k}{\sqrt{2}\sigma}
\right)
-
\operatorname{erfc}
\left(
\frac{\ln k_{i,\mathrm{right}}-\ln k}{\sqrt{2}\sigma}
\right)
\right].
\]

This parameterization allowed the primordial tensor power to vary independently across different scales.

![Scale-dependent primordial tensor spectrum]({{ '/research/cmb-s4/scale-dependent-spectrum.jpg' | relative_url }})

*Smooth logarithmic bins used to construct the scale-dependent primordial tensor power spectrum.*

---

## Numerical Pipeline

I developed a Python pipeline that connected the primordial tensor spectrum to the expected CMB B-mode observables.

The main stages were:

1. Construct a scale-dependent primordial tensor power spectrum.
2. Modify the relevant primordial-spectrum inputs to CLASS.
3. Use CLASS to calculate the corresponding CMB B-mode angular power spectrum.
4. Vary the tensor amplitude in each logarithmic \(k\)-bin.
5. Calculate numerical derivatives of the B-mode spectrum with respect to each model parameter.
6. Construct the Fisher-information matrix.
7. Marginalize over nuisance parameters, including the residual lensing amplitude.
8. Convert the forecast constraints into constraints on the primordial gravitational-wave energy density.

---

## Fisher-Matrix Forecasting

The Fisher-information matrix estimates the parameter sensitivity of an experiment around a chosen fiducial model.

For parameters \(\theta_i\) and \(\theta_j\), the B-mode Fisher matrix may be written schematically as

\[
F_{ij}
=
\sum_{\ell}
\frac{2\ell+1}{2}f_{\mathrm{sky}}
\frac{
\displaystyle
\frac{\partial C_\ell^{BB}}{\partial\theta_i}
\frac{\partial C_\ell^{BB}}{\partial\theta_j}
}{
\left(C_{\ell,\mathrm{tot}}^{BB}\right)^2
},
\]

where:

- \(f_{\mathrm{sky}}\) is the observed sky fraction,
- \(C_\ell^{BB}\) is the modeled B-mode power spectrum,
- \(C_{\ell,\mathrm{tot}}^{BB}\) includes signal, residual lensing, foregrounds, and instrumental noise.

The inverse Fisher matrix approximates the covariance matrix:

\[
\mathrm{Cov}(\theta_i,\theta_j)\approx(F^{-1})_{ij}.
\]

The marginalized forecast uncertainty is then

\[
\sigma(\theta_i)\approx\sqrt{(F^{-1})_{ii}}.
\]

The forecast included assumptions about:

- Sky coverage
- Instrumental noise
- Galactic foreground noise
- Residual gravitational lensing
- The accessible multipole range

---

## Preliminary Constraints

The preliminary calculation found that the strongest sensitivity occurred around

\[
k \approx 0.01\ {\rm Mpc}^{-1}.
\]

This scale is close to the comoving horizon scale near matter–radiation equality.

For the most sensitive scale bin, the poster reported the preliminary uncertainties

\[
\sigma_r \approx 6.344\times10^{-5}
\]

and

\[
\sigma_{P_t(k)} \approx 1.394\times10^{-13}.
\]

These values were preliminary and depended on the fiducial spectrum, binning scheme, experimental assumptions, treatment of foregrounds, and delensing model.

The constraints on the tensor spectrum were also converted into constraints on the gravitational-wave energy density, \(\Omega_{\mathrm{GW}}(k)\), and compared with previously published CMB upper limits.

<img
  src="/research/cmb-s4/cmb-map.jpg"
  alt="Cosmic microwave background temperature anisotropies"
  style="display: block; width: 100%; height: auto; margin: 1.5em auto 0.5em;"
>

*Preliminary scale-dependent forecast constraints converted into limits on the primordial gravitational-wave energy density.*




---

## Delensing

Gravitational lensing by large-scale structure remaps the CMB polarization field and converts part of the E-mode signal into B modes.

This lensing-induced B-mode signal can obscure the primordial tensor contribution. The effect is particularly important when searching for a small primordial signal.

I parameterized the residual lensing contribution using \(A_L\):

\[
C_{\ell,\mathrm{tot}}^{BB}
=
r\,C_{\ell,\mathrm{tensor}}^{BB}(r=1)
+
A_L C_{\ell,\mathrm{lens}}^{BB}
+
N_\ell^{BB}
+
C_{\ell,\mathrm{foreground}}^{BB}.
\]

Here:

- \(A_L=1\) represents the full lensing B-mode power,
- \(A_L=0.1\) represents 10% residual lensing power,
- \(A_L=0\) represents idealized perfect delensing.

The forecast showed that larger residual lensing amplitudes increase the uncertainty in \(r\), particularly when the primordial signal is small.

![Forecast uncertainty under different delensing assumptions]({{ '/research/cmb-s4/delensing-forecast.jpg' | relative_url }})

*Forecast uncertainty as a function of the tensor-to-scalar ratio for different residual lensing amplitudes.*

---

## Main Findings

This preliminary analysis demonstrated that:

- A scale-dependent primordial tensor spectrum can be propagated through CLASS and constrained using CMB B-mode observations.
- CMB-S4 sensitivity is not uniform across wavenumber.
- The strongest sensitivity in this setup occurred near \(k\approx0.01\ {\rm Mpc}^{-1}\).
- Residual lensing significantly affects forecasts for small tensor amplitudes.
- Delensing is essential for improving sensitivity to primordial B modes.
- A binned analysis can test tensor spectra that are not adequately described by a single tensor-to-scalar ratio.

---

## My Contributions

My work on this project included:

- Using the public Boltzmann code CLASS to calculate CMB temperature and polarization power spectra.
- Developing Python tools to generate scale-dependent primordial tensor spectra.
- Constructing 15 smooth logarithmic tensor-power bins.
- Calculating the corresponding CMB B-mode spectra.
- Computing numerical derivatives for Fisher-matrix forecasts.
- Forecasting constraints on \(r\) and \(P_t(k)\).
- Including sky coverage, instrumental noise, foreground noise, and residual lensing in the forecast.
- Marginalizing over the residual lensing amplitude \(A_L\).
- Converting tensor-spectrum constraints into limits on \(\Omega_{\mathrm{GW}}\).
- Preparing and presenting the results as an interactive poster at AAS 241.

---

## Future Work

The next stages identified in the project were:

- Generate delensed spectra using **CLASS_DELENS**.
- Improve the treatment of Galactic and extragalactic foregrounds.
- Include additional cosmological and nuisance parameters.
- Model correlations between scale bins.
- Refine the treatment of both low- and high-multipole data.
- Compare Fisher forecasts with posterior constraints from Markov Chain Monte Carlo methods.
- Test the robustness of the constraints under different fiducial tensor spectra and experimental assumptions.

---

## Methods and Tools

**Physics:** Cosmic microwave background, inflation, primordial gravitational waves, tensor perturbations, B-mode polarization, gravitational lensing

**Computation:** Python, CLASS, numerical derivatives, scientific visualization

**Statistics:** Fisher-information matrices, covariance analysis, parameter marginalization, scale-dependent forecasting

---

## Poster and Code

<a class="btn btn-default btn-lg"
   href="https://aas241-aas.ipostersessions.com/Default.aspx?s=73-8F-44-9D-6A-D0-58-4A-2F-96-42-B6-AF-88-A7-15"
   target="_blank"
   rel="noopener noreferrer">
  <i class="fa fa-picture-o"></i> Open the AAS 241 Poster
</a>

<a class="btn btn-default btn-lg"
   href="https://github.com/HeidiYLiu/omega_gw-constraints"
   target="_blank"
   rel="noopener noreferrer">
  <i class="fa fa-github"></i> View the Project Code
</a>

---

[← Back to Research]({{ '/research/' | relative_url }})
