# Time-parametric Gerstner Wave Engine for Digital Craft

Grasshopper and GhPython definitions for a generative wave-surface system that bridges
computational design with physical fabrication. This repository is the supplementary
material for the paper cited below: a Python engine that extends the classical Gerstner
wave equation with multi-octave layering, domain warping, and a continuous time variable
`t` treated as a design parameter, used to generate a surface subsequently machined in
solid brass.

## Citation

> Min, B. (2026). Algorithmic waves and physical Moiré: Time-parametric generative design
> and the dialectic of digital craftsmanship. In *Proceedings of the XXX Conference of the
> Iberoamerican Society of Digital Graphics (SIGraDi 2026)*. (to appear)

## Relationship to the Paper

The paper describes the engine's development as **five stages** (Fig. 2). This repository
contains the **nine definition files** of the complete, unedited working sequence.

The two are not in conflict: the five stages of the paper are *conceptual* — each marks the
point at which a new formal principle enters the engine — while the nine files are the
*implementation* iterations through which those principles were built and tuned. Several
files therefore belong to a single conceptual stage, and the final three introduce no new
principle at all.

| Paper stage (Fig. 2) | Principle introduced | File(s) |
| --- | --- | --- |
| ① Single-direction Gerstner | Trochoidal profile; ridge steepness | `01_gerstner-base.ghx` |
| ② Free direction, two-octave | Anisotropy; swell with masked ripple | `02_wind-octave.ghx` |
| ③ Spatial falloff, crest lean, turbulence | Non-uniform distribution of wave energy | `03_falloff-lean-turb.ghx` |
| ④ Five-octave golden-angle superposition | Fractal self-similarity across scales | `04_directional-interference.ghx`, `05_spread-control.ghx` |
| ⑤ Clumping and domain warping | Macro-scale irregularity; nonlinear refraction | `06_full-engine.ghx` |
| — | No new principle: preset selection and render setup | `07_engine-preset-a.ghx`, `08_engine-render.ghx`, `09_engine-render-final.ghx` |

Each addition answered a specific perceptual dissatisfaction rather than an arbitrary
expansion of the parameter set: ridges too regular led to golden-angle dispersion, energy
too uniform to clumping, flow too linear to domain warping.

## Requirements

- Rhino 7 or 8 with Grasshopper
- GhPython component (included with Grasshopper)
- Native Grasshopper components only — no third-party plug-ins required

## Usage

Supply a point grid and a time value `t` to the GhPython component, adjust the parameter
sliders, and the component returns displaced points from which the surface is built. Set
the `U` count of *Surface from Points* to the grid's X-direction point count (`Ex + 1`),
with the point list flattened.

## Parameters

The final engine (`06_full-engine.ghx`) exposes user controls in five groups:

- **Geometric** — amplitude, wavelength, steepness
- **Environmental** — wind direction, spread, lean
- **Stochastic** — noise intensity, noise scale, seed, turbulence
- **Compositional** — falloff, clumping, warp
- **Layering** — energy decay, frequency step

The time variable `t` is not a playback control but an independent design variable over a
continuous real-valued domain: a particular instant `t₀` is selected by aesthetic judgment
and fixed as the form to be machined.

## Reproducing the Published Result

`09_engine-render-final.ghx` holds the preset configuration used for the brass artifact
shown in the paper, with all parameter values and the selected time value embedded
directly in the definition's sliders.

## License

Released under the MIT License. See [LICENSE](LICENSE).
