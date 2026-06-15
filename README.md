# Time-parametric Gerstner Wave Engine for Digital Craft

Grasshopper / GhPython definitions accompanying the paper on a hybrid
generative-to-fabrication workflow, in which an extended Gerstner-wave model is
treated not as a closed geometric tool but as a medium for artistic intent. A
time-parametric Python engine generates an evolving wave surface; a chosen
"temporal moment" is then frozen and realized in solid brass through
craft-based CNC machining.

This repository documents the **iterative development of the wave-generation
algorithm** as a sequence of nine saved Grasshopper definitions, from the first
single-direction wave to the final 17-parameter engine and its presentation
presets.

> Authorship and DOI are omitted in this review copy for double-blind review. A
> permanent, citable archive (with DOI) will be released upon acceptance.

## Requirements

- **Rhino 7 or Rhino 8** with Grasshopper.
- **GhPython** (the script component shipped with Grasshopper; no external
  plugin required).
- The definitions use only native Grasshopper components plus one GhPython
  component.

The scripts were authored in Rhino 7 (GhPython 7.38, IronPython 2.7). In Rhino 8
they load in the legacy GhPython component (labelled "old") and run unchanged;
the code is also compatible with the Rhino 8 Python 3 script component without
modification.

## How to use

1. Open any `.ghx` file in Grasshopper.
2. Feed a grid of points into the `pts` input and a time value into `t`.
3. Adjust the parameter sliders; the script returns displaced points (`a`),
   which are lofted into a surface by the `Surface From Points` component.
4. Files `08` and `09` add a colour/material `Custom Preview` layer for
   presentation views.

## Version history

The numbering follows the order in which the versions were saved during
development.

| File | Function | Params | What it adds |
|------|----------|:------:|--------------|
| `01_gerstner-noise.ghx` | `generate_natural_wave_2d` | 7 | Base Gerstner wave with composite XY phase and mathematical noise |
| `02_wind-octave.ghx` | `generate_ocean_wave` | 9 | Wind direction (`wind_dir`), seed, two-octave layering (swell + detail ripple) |
| `03_falloff-lean-turb.ghx` | `generate_advanced_ocean` | 12 | Spatial damping (`falloff`), non-linear lean, micro-turbulence |
| `04_directional-interference.ghx` | `generate_complex_ocean` | 12 | Switch to three-directional wave interference (60% / 25% / 15%) |
| `05_spread-control.ghx` | `generate_custom_ocean` | 13 | `spread` parameter to control energy/angle distribution of the interference |
| `06_full-engine.ghx` | `generate_ultimate_ocean` | 17 | Five-octave golden-angle layering (`energy_decay`, `freq_step`), energy clumping, domain warping — the complete engine |
| `07_engine-preset-a.ghx` | (same code as `06`) | 17 | Engine with an alternative slider preset |
| `08_engine-render.ghx` | (same code as `06`) | 17 | Engine plus a colour / material / Custom Preview rendering layer |
| `09_engine-render-final.ghx` | (same code as `06`) | 17 | Rendering layer; **the preset used to produce the published brass artifact** |

Files `07`–`09` share the identical algorithm of `06`; they differ only in
slider values and (for `08`/`09`) an added presentation layer. The algorithm
itself stops evolving at `06`.

## Algorithm evolution

1. **Foundation** — a single-direction Gerstner wave with horizontal (X, Y) and
   vertical (Z) displacement, controlling ridge steepness.
2. **Environment & layering** — free wave heading plus octave stacking (large
   swell carrying smaller ripples), with noise masking for organic, uneven
   amplitude.
3. **Physics & spatial control** — edge damping for fabrication stability,
   non-linear lean for a dynamic spilling silhouette, and micro-turbulence for
   optical surface texture.
4. **Interference & intelligence** — multi-directional superposition advancing to
   five-octave layering distributed by the golden angle, forming independent
   peaks with fractal-like complexity from few parameters.
5. **Macro-stochasticity** — energy clumping for large-scale rhythm across the
   plate, and domain warping to bend the flow into fluid, meandering ridges.

## Parameters

The final engine exposes 15 user controls (besides the `pts` and `t` inputs).
Fourteen are organised as follows:

- **Geometric** — `amp`, `wavelength`, `steepness`
- **Environmental** — `wind_dir`, `spread`, `lean`
- **Stochastic** — `n_intensity`, `seed`, `turbulence`
- **Composition** — `falloff`, `clumping`, `warp`
- **Intelligent** — `energy_decay`, `freq_step`

### Note on `n_scale`

`n_scale` controls the noise frequency in versions `01`–`02`. From version `03`
onward the noise/turbulence frequency was hard-coded, so `n_scale` remains as a
function argument but no longer affects the output (its slider is inert). It is
kept to preserve the authentic development history and is intentionally not part
of the parameter taxonomy above.

## Reproducing the published artifact

The complete engine is `06_full-engine.ghx`. The published brass piece was
produced by `09_engine-render-final.ghx`, a preset of that engine, with the
wave surface frozen at a single time value `t`. The exact parameter values and
the value of `t` are stored directly in the sliders of that definition — open
`09_engine-render-final.ghx` in Grasshopper to read them.

## Citation and license

- Citation: _[author / venue / DOI to be added upon publication]_
- License: _[MIT for the code and CC BY 4.0 for the design output]_
