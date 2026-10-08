# Degenerate Fermi Gases, Interactively

An interactive, single-page web demo of the degenerate Fermi gas: fermions packed into the lowest available states, the Fermi energy, degeneracy pressure in metals and stars, and what happens at small nonzero temperatures.

Created by **Claude Opus 5.5**, based on the lecture notes by **Sang Hoon Lee** (Chapter 7, Quantum Statistics; Section 7.3, Degenerate Fermi Gases). It is a companion to the demos for Section 7.1 (the grand canonical ensemble) and Section 7.2 (bosons and fermions).

## What's inside

**Filling the Fermi sea.** Add electrons one at a time to the *n*-space lattice and watch them fill the lowest energies first, two spins per state. The default 3D view shows the occupied lattice points forming an eighth of a sphere, with the continuum radius n<sub>max</sub> = (3N/π)<sup>1/3</sup> drawn as a wireframe; it rotates slowly and can be turned by dragging or with the arrow keys. A 2D slice shows the same idea as a quarter of a disk. The exact Fermi energy and average energy from counting lattice points are compared with the continuum results, ε<sub>F</sub> = (3N/π)<sup>2/3</sup> and U = (3/5) Nε<sub>F</sub> in 3D, or ε<sub>F</sub> = 2N/π and U = ½ Nε<sub>F</sub> in 2D (in units of h²/8mL²). The text then derives the three-dimensional results in physical units:

```
ε_F = (h²/8m) (3N/πV)^(2/3),     U = (3/5) N ε_F
```

**Electrons in metals.** Degeneracy pressure P = 2U/3V and the bulk modulus B = (10/9) U/V, computed from the conduction-electron density of seven metals (Li, Na, K, Cu, Ag, Au, Al) and compared with measured bulk moduli on a log-scale chart. Copper gives ε<sub>F</sub> ≈ 7.0 eV, T<sub>F</sub> ≈ 81,600 K, and B ≈ 64 GPa against a measured 140 GPa.

**Stars held up by the exclusion principle.** Problems 7.22 to 7.24. Plot U<sub>kinetic</sub> ∝ 1/R², U<sub>grav</sub> ∝ −1/R, and their sum for a white dwarf or a neutron star of adjustable mass, and read off the equilibrium radius R<sub>eq</sub> ∝ M<sup>−1/3</sup>, density, Fermi energy, and Fermi temperature. For one solar mass (2 × 10<sup>30</sup> kg, as in the lecture):

| Quantity | White dwarf | Neutron star |
| --- | --- | --- |
| R<sub>eq</sub> | 7.2 × 10<sup>6</sup> m | 12.3 km |
| Density | 1.3 × 10<sup>9</sup> kg/m³ | 2.6 × 10<sup>17</sup> kg/m³ |
| ε<sub>F</sub> | 1.9 × 10<sup>5</sup> eV | 5.7 × 10<sup>7</sup> eV |
| T<sub>F</sub> | 2.3 × 10<sup>9</sup> K | 6.6 × 10<sup>11</sup> K |
| Becomes relativistic at | about 3 M<sub>⊙</sub> | about 12 M<sub>⊙</sub> |

The relativistic case, where U<sub>kinetic</sub> also scales as 1/R and no stable radius exists, is explained alongside.

**A little bit of heat.** The density of states g(ε) ∝ √ε, the occupied region g(ε) n̄<sub>FD</sub>(ε) at an adjustable temperature, and the resulting shift of μ below ε<sub>F</sub>. The demo solves the number and energy integrals numerically and compares them with the Sommerfeld expansion:

```
μ/ε_F ≈ 1 − (π²/12)(k_B T/ε_F)²,     U ≈ (3/5) N ε_F + (π²/4) N (k_B T)²/ε_F,     C_V = π² N k_B² T / 2ε_F
```

Charts of μ(T) and C<sub>V</sub>(T) show the crossover from the degenerate regime to the classical limit (C<sub>V</sub> → 3/2 Nk<sub>B</sub>). A switch selects the two-dimensional gas of Problems 7.28 and 7.31, with its constant density of states, exact μ = k<sub>B</sub>T ln(e<sup>ε<sub>F</sub>/k<sub>B</sub>T</sup> − 1), and C<sub>V</sub> → Nk<sub>B</sub>.

## Running it

There is nothing to build or install. The whole demo is one self-contained file, `index.html`, with all CSS and JavaScript inline.

Open it locally by double-clicking `index.html`, or serve the folder:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

### Publishing with GitHub Pages

1. Push this repository to GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, select your main branch and the `/ (root)` folder, then save.
4. After a minute or so, the demo will be live at `https://<your-username>.github.io/<repository-name>/`.

## Technical notes

- Plain HTML, CSS, and vanilla JavaScript drawn on `<canvas>`. No frameworks, no build step.
- The 3D *n*-space view is a lightweight hand-written projection (rotation plus mild perspective, drawn far to near) rather than a 3D library. Rotation pauses when the view is off screen and is off by default when the system asks for reduced motion.
- The finite-temperature curves are computed in the browser: μ(T) by bisection on the Fermi–Dirac number integral, and U(T) by Simpson's rule, with C<sub>V</sub> from a finite difference. The three-dimensional table takes a fraction of a second to build on page load.
- Equations are typeset with [MathJax 3](https://www.mathjax.org/) (SVG output, loaded from cdnjs), so they need no extra web fonts.
- The only other external resources are the Newsreader and Instrument Sans fonts from Google Fonts, with system font fallbacks if they fail to load.
- Opening the page requires an internet connection for MathJax; offline, the equations appear as raw TeX.
- Supports light and dark mode: it follows `prefers-color-scheme`, and a sun/moon button in the top-right corner switches by hand (the choice is remembered across pages); and is responsive down to phone widths.
- Constants used: h = 6.626 × 10<sup>−34</sup> J s, k<sub>B</sub> = 1.381 × 10<sup>−23</sup> J/K, G = 6.674 × 10<sup>−11</sup> N m²/kg², M<sub>⊙</sub> = 2 × 10<sup>30</sup> kg.

## Caveats

- Conduction-electron densities and measured bulk moduli are typical handbook values; different sources differ by a few percent.
- The star model is the lecture's: a uniform-density sphere at T = 0 with nonrelativistic particles. A fuller relativistic treatment gives the Chandrasekhar limit of about 1.4 M<sub>⊙</sub> for white dwarfs, and real neutron stars also require general relativity and nuclear forces.
- The interior temperatures quoted for comparison (about 10<sup>7</sup> K for a white dwarf and 2 × 10<sup>6</sup> K for a neutron star) are the rough values used in the lecture.

## Credits

- Demo: Claude Opus 5.5
- Physics content and examples: lecture notes by Sang Hoon Lee
- The lecture follows Daniel V. Schroeder, *An Introduction to Thermal Physics* (Problems 7.22, 7.23, 7.24, 7.28, 7.29, and 7.31).

## License

No license has been chosen yet. Add a `LICENSE` file (for example, MIT or CC BY 4.0) before sharing or reusing this project publicly, and confirm that any use of the lecture material is permitted by its author.
