---
layout: blog_post
title: "Full Vectorial Control of Arbitrary Optical Fields"
date: 2026-07-01
tags:
  - Structured Light
  - SLM
  - Polarisation Control
---

<p class="project-lede">
This fourth-year master's project studies how to generate arbitrary vectorial optical fields with programmable SLM-based systems. The goal is simultaneous spatial control of intensity, phase, and polarisation, rather than treating them as separate degrees of freedom.
</p>

<p class="project-actions">
  <a class="btn btn-sm btn-outline-primary" target="_blank" href="{{ '/assets/pdf/reports/full-vectorial-control-4yp-report.pdf' | relative_url }}">
    <i class="fas fa-file-pdf"></i> View full 4YP report
  </a>
</p>

## Aim

A general vectorial field can be described by a spatially varying Jones vector,

$$
\mathbf{E}(x,y,z,t)=
\operatorname{Re}
\left[
\begin{pmatrix}
E_x(x,y,z) \\
E_y(x,y,z)
\end{pmatrix}
e^{i(kz-\omega t)}
\right].
$$

The practical challenge is that an SLM does not directly display an arbitrary complex vector field. It typically modulates phase for one linear polarisation component. The project therefore asks: how many programmable phase planes are needed, how should they be arranged optically, and how can their phase patterns be made experimentally displayable?

<div class="project-summary-grid">
  <div class="project-summary-card">
    <strong>Question</strong>
    <span>Can arbitrary vectorial optical fields be generated with phase-only programmable optics?</span>
  </div>
  <div class="project-summary-card">
    <strong>Method</strong>
    <span>Jones calculus, Poincare-sphere reasoning, inverse design, and phase-pattern optimisation.</span>
  </div>
  <div class="project-summary-card">
    <strong>Validation</strong>
    <span>Numerical phase synthesis followed by experimental Stokes reconstruction.</span>
  </div>
</div>

## Four-SLM baseline

The first architecture uses four SLMs. In the report's decomposition, the early stages control global phase and intensity, while the later stages synthesize the desired polarisation state. The model is built from standard Jones elements:

$$
P(\alpha)=
\begin{pmatrix}
\cos^2\alpha & \cos\alpha\sin\alpha \\
\cos\alpha\sin\alpha & \sin^2\alpha
\end{pmatrix},
$$

$$
R(\theta)=
\begin{pmatrix}
\cos\theta & \sin\theta \\
-\sin\theta & \cos\theta
\end{pmatrix},
\qquad
W(\theta,\Delta)=
R(-\theta)
\begin{pmatrix}
e^{-i\Delta/2} & 0 \\
0 & e^{i\Delta/2}
\end{pmatrix}
R(\theta).
$$

<figure class="research-figure">
  <img src="{{ '/assets/images/research/full-vectorial-control/four-slm-architecture.jpg' | relative_url }}" alt="Four-SLM architecture for vectorial optical field control">
  <figcaption>
    Four-SLM architecture. It is mathematically capable of local vectorial control, but the inverse solution can produce abrupt phase jumps on the displayed SLM patterns.
  </figcaption>
</figure>

The central limitation is not that the target vector field is impossible. The limitation is inverse-design conditioning: when the target contains azimuthal winding or singular structure, the direct 4-SLM decomposition can force discontinuities into the SLM phase maps. Those phase jumps are hard for a real optical system to reproduce cleanly.

## Five-SLM strategy

The report then extends the architecture by adding a fifth SLM into the polarisation synthesis block. This extra programmable plane acts like an internal degree of freedom: it preserves the target output field while allowing the algorithm to redistribute troublesome phase structure across the system.

<figure class="research-figure">
  <img src="{{ '/assets/images/research/full-vectorial-control/five-slm-architecture.jpg' | relative_url }}" alt="Five-SLM architecture for vectorial optical field control">
  <figcaption>
    Five-SLM architecture. The added SLM makes the inverse problem less rigid, giving the design algorithm room to avoid the most damaging phase discontinuities.
  </figcaption>
</figure>

In compact form, the full optical train can be written as a product of SLM phase operators, polarisers, and half-wave plates:

$$
J_{\mathrm{tot}} =
J_{\mathrm{SLM5}}(\phi_5)
W_{\mathrm{HWP}}(22.5^{\circ})
J_{\mathrm{SLM4}}(\phi_4)
W_{\mathrm{HWP}}(22.5^{\circ})
J_{\mathrm{SLM3}}(\phi_3)
P(-45^{\circ})
J_{\mathrm{SLM2}}(\phi_2)
P(45^{\circ})
J_{\mathrm{SLM1}}(\phi_1).
$$

The target polarisation ratio can be parameterised as

$$
r_t=e^{i\delta}\tan\gamma.
$$

Introducing the fifth phase map changes the internal ratio to

$$
r' = e^{i(\delta-\phi_5)}\tan\gamma,
\qquad
u =
i\frac{1-\tan\gamma e^{i(\delta-\phi_5)}}{1+\tan\gamma e^{i(\delta-\phi_5)}}.
$$

This gives phase solutions such as

$$
\phi_4=\arg(u),
\qquad
\phi_3=2\arctan |u|.
$$

The important design insight is that $\phi_4$ is no longer tied directly to the target relative phase $\delta$. By optimising $\phi_5$, the system can move branch structure away from visually and experimentally sensitive regions.

## Optimisation

The fifth SLM phase is treated as an optimisation variable, represented with a low-frequency basis:

$$
\phi_5(x,y)=\sum_m c_m B_m(x,y).
$$

The report minimises a loss that balances singularity avoidance and phase-range constraints:

$$
\mathcal{L}
=
\mathcal{L}_{\mathrm{sing}}(r_t,\phi_5)
+\lambda_1\mathcal{L}_{\mathrm{range},4}(\phi_4)
+\lambda_2\mathcal{L}_{\mathrm{range},5}(\phi_5).
$$

<figure class="research-figure">
  <img src="{{ '/assets/images/research/full-vectorial-control/optimised-phase-maps.jpg' | relative_url }}" alt="Optimised phase maps for four-SLM and five-SLM vectorial field generation">
  <figcaption>
    Optimised phase maps. Compared with the direct 4-SLM decomposition, the 5-SLM design redistributes phase structure and removes much of the visible discontinuity from the primary SLM patterns.
  </figcaption>
</figure>

This does not magically remove every singularity from every possible target field. Instead, it turns a rigid algebraic inverse into an engineering design problem: the unavoidable non-smooth structure can be placed where it is less harmful for the final optical field.

## Experimental validation

The project tested the generated patterns on a cascaded-SLM optical platform using Stokes reconstruction. Target fields with one-edge and two-edge structures retained their main polarisation organisation in the measured output, with no strong line artefact directly matching the original 4-SLM discontinuity.

<div class="project-summary-grid">
  <div class="project-summary-card">
    <strong>One-edge field</strong>
    <span>Mean angular error: 13.9462% of a 180 degree scale.</span>
  </div>
  <div class="project-summary-card">
    <strong>Two-edge field</strong>
    <span>Mean angular error: 10.5744% of a 180 degree scale.</span>
  </div>
  <div class="project-summary-card">
    <strong>Main residuals</strong>
    <span>Largest errors appear near singular regions and from calibration, registration, and camera noise.</span>
  </div>
</div>

<figure class="research-figure">
  <img src="{{ '/assets/images/research/full-vectorial-control/stokes-validation.jpg' | relative_url }}" alt="Experimental Stokes reconstruction for vectorial optical fields">
  <figcaption>
    Stokes-reconstruction validation. The measured vectorial fields reproduce the target organisation well enough to show that the optimised phase patterns survive the real optical system.
  </figcaption>
</figure>

## Why it matters

The project reframes full vectorial field control as both an optical architecture problem and an inverse-design problem. A 4-SLM system is a useful theoretical baseline, but the 5-SLM system is more experimentally robust because the extra degree of freedom can regularise the phase maps before they are displayed.

<div class="research-callout">
  Beyond free-space SLM control, the same vectorial-field language connects to waveguide mode engineering and the broader work on generalized optical skyrmions: if the full local field vector can be generated and measured reliably, more complex topological light states become experimentally accessible.
</div>
