---
layout: blog_post
title: "The Use of Femtosecond Laser Written Directional Couplers for Polarimeter Application"
date: 2024-08-01
tags:
  - Polarimetry
  - Directional Couplers
  - Femtosecond Laser Writing
---

<p class="project-lede">
This project investigates whether femtosecond-laser-written directional couplers can act as compact polarimetric elements: not only splitting optical power between two waveguides, but doing so in a way that encodes the input polarisation state.
</p>

<p class="project-actions">
  <a class="btn btn-sm btn-outline-primary" target="_blank" href="{{ '/assets/pdf/reports/directional-couplers-polarimeter-report.pdf' | relative_url }}">
    <i class="fas fa-file-pdf"></i> View full research report
  </a>
</p>

## Core idea

In an ideal directional coupler, light launched into one waveguide periodically transfers to the neighbouring guide. If the coupling strength is different for the two orthogonal polarisation components, the output splitting ratio becomes polarisation dependent. The project asks whether that effect can be calibrated well enough to recover useful polarisation information from a small laser-written device.

<div class="project-summary-grid">
  <div class="project-summary-card">
    <strong>Device</strong>
    <span>Femtosecond-laser-written directional couplers in borosilicate glass.</span>
  </div>
  <div class="project-summary-card">
    <strong>Dataset</strong>
    <span>40+ fabricated couplers and more than 500 splitting-ratio measurements.</span>
  </div>
  <div class="project-summary-card">
    <strong>Outcome</strong>
    <span>A calibrated model that predicts output ratios and narrows the possible input polarisation states.</span>
  </div>
</div>

## Coupled-mode model

The model starts from two weakly guiding, near-identical waveguides. Under the usual coupled-mode assumptions, the normalised power oscillates between arms:

$$
\tilde{P}_a(z)=1-F\sin^2(\gamma z),
\qquad
\tilde{P}_b(z)=F\sin^2(\gamma z).
$$

For a fabricated interaction region of length $L_0$, the measured splitting ratio can be written as a weighted combination of the responses for two orthogonal polarisation axes:

$$
r(L_0,\theta)=
\sin^2\left(\frac{k_xL_0}{2}\right)
+ \sin^2\theta
\left[
\sin^2\left(\frac{k_yL_0}{2}\right)
- \sin^2\left(\frac{k_xL_0}{2}\right)
\right].
$$

Here $k_x$ and $k_y$ are the fitted coupling coefficients for the two axes, while $\theta$ is the input linear polarisation angle. Once $k_x$ and $k_y$ are calibrated, the relation can be inverted:

$$
\theta =
\arcsin
\sqrt{
\frac{
r-\sin^2(k_xL_0/2)
}{
\sin^2(k_yL_0/2)-\sin^2(k_xL_0/2)
}
}.
$$

<p class="research-formula-note">
This inverse is not single-valued: the same splitting ratio can correspond to two symmetric polarisation angles, so a phase-sensitive element would be needed for a fully unique polarimeter.
</p>

<figure class="research-figure">
  <img src="{{ '/assets/images/research/directional-couplers/model-and-device.jpg' | relative_url }}" alt="Directional coupler geometry and coupled-mode model">
  <figcaption>
    Model and device geometry. The project varied interaction length and waveguide separation, then used the measured output power ratio to fit polarisation-dependent coupling coefficients.
  </figcaption>
</figure>

## Fabrication and measurement

The devices were written into Corning Eagle2000 borosilicate glass using femtosecond laser writing, then polished for end-fire coupling. The design sweep covered interaction lengths from 2 mm to 10 mm and several inter-waveguide separations, including 0.008 mm, 0.006 mm, and 0.004 mm.

Each coupler was measured under multiple input polarisation angles. A typical measurement series used a 780 nm laser, controlled input power, and a Thorlabs PM100D power meter to record the output powers from both arms. For one separation-length sweep, 17 interaction lengths and 7 polarisation settings produced 119 splitting-ratio measurements.

## Calibration and fit quality

The fitting workflow used constrained optimisation to estimate $k_x$, $k_y$, length shift, angle shift, and ambient-power correction terms. This matters because small fabrication offsets and background power can otherwise be misread as physics.

<figure class="research-figure">
  <img src="{{ '/assets/images/research/directional-couplers/model-fit-comparison.jpg' | relative_url }}" alt="Measured and fitted splitting ratios for directional couplers">
  <figcaption>
    Representative model fits. The 0.006 mm separation data reached about 0.87% mean squared error, and the 3.5 mm interaction length gave a strong polarisation-sensitive slope.
  </figcaption>
</figure>

For the polarimeter calibration stage, the report fitted the measured splitting-ratio curve with parameters including angle shift and ambient power. One calibrated run reached a minimum mean squared error of 0.00018, or 0.018%, showing that the model can track the experimental response closely after calibration.

<div class="project-summary-grid">
  <div class="project-summary-card">
    <strong>Best separation fit</strong>
    <span>0.006 mm separation, approximately 0.87% MSE for the fitted sweep.</span>
  </div>
  <div class="project-summary-card">
    <strong>Polarimeter fit</strong>
    <span>Minimum MSE of 0.00018 after calibration.</span>
  </div>
  <div class="project-summary-card">
    <strong>Prediction spread</strong>
    <span>Mean prediction-measurement difference of -0.000285 with standard deviation 0.013855.</span>
  </div>
</div>

<figure class="research-figure">
  <img src="{{ '/assets/images/research/directional-couplers/prediction-measurement-table.jpg' | relative_url }}" alt="Predicted and measured splitting ratios for polarimeter calibration">
  <figcaption>
    Predicted versus measured splitting ratios after calibration. The close agreement supports using the directional coupler response as a compact polarisation diagnostic, while also showing where ambiguity remains.
  </figcaption>
</figure>

## What the project shows

The key result is that femtosecond-laser-written directional couplers can be engineered and calibrated to behave as compact polarisation-sensitive elements. The device does not yet determine a unique full polarisation state by itself, because intensity splitting alone cannot distinguish all equivalent angle solutions. Still, it can reduce the problem to a small set of candidate states and provides a clear path toward a fuller polarimeter by adding phase information.

The model also predicts when the device becomes polarisation independent. A non-trivial independence condition occurs when

$$
\sin^2\left(\frac{k_yL_0}{2}\right)
=
\sin^2\left(\frac{k_xL_0}{2}\right),
\qquad
L_0 = \frac{2n\pi}{|k_x-k_y|}.
$$

That is useful in two ways: such lengths should be avoided when building a polarimeter, but they may be deliberately chosen when a polarisation-insensitive splitter is desired.

<div class="research-callout">
  This work contributed to a co-authored Optics Communications paper and gave a practical bridge between coupled-mode theory, femtosecond laser fabrication, and calibration-driven photonic sensing.
</div>
