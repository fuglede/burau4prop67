# Braid Atlas — reconstructed source ZIP

This is a **standalone reconstruction** of the Braid Atlas walkthrough discussed in the ChatGPT conversation. It is **not an export of the original project's exact source code**: the original hosted site's source repository was not accessible in the environment used to prepare this ZIP.

The replacement implements the key functions described in the conversation:

- Six interactive proof-review steps, addressable with `#step/0` through `#step/5`.
- The explicit 26-letter Artin-generator counterexample and its factorization.
- The proper-product geometric *certificate*, including `30 + 5 × 46 = 260` crossings.
- The exact 4×4 unreduced Burau matrix for any editable braid word, evaluated at `t = -1` or `t = 2`, calculated **in the browser using BigInt rational arithmetic**.
- Interactive strand diagram, step-by-step word prefix slider, parity-condition toggles, and a downloadable JSON matrix certificate.
- A discussion of exactly where the unequal-intersection conclusion in Proposition 6.7 is obstructed.

## How to run

**No dependencies and no build step are required.** Extract the ZIP and open `index.html` in a modern browser. For an optional local web server:

```bash
cd braid-atlas-source
python3 -m http.server 8000
# Open http://localhost:8000/
```

## Files

- `index.html` — semantic content/layout and app controls.
- `styles.css` — responsive dark-theme design.
- `app.js` — exact matrix arithmetic, braid diagram, step navigation, parity logic, and event handlers.
- `README.md` — usage, verification, and limitations.
- `LICENSE` — MIT license for this reconstruction.

## Reproducing the test

The app automatically checks that the original 26-letter word yields

```
R4(Phi)(-1) = identity(4)
R4(Phi)(2)[1,1] = -3419/64
30 + 5 * 46 = 260
```

The `t=2` entry uses 1-based mathematical indexing; it is `matrix[0][0]` in source code.

Default word:

```
s2^-2 s1^3 s2^2 s1^2 s2 s3^-2 s2^-1 s1^-2 s2^-2 s1^-2 s2^-1 s3^2 s2 s1^-1 s2^2
```

The Artin/Burau conventions are

```
sigma_i: x_i -> x_i x_(i+1) x_i^-1; x_(i+1) -> x_i
R(sigma_i) on indices (i,i+1) = [[1-t, t], [1, 0]]
```

## Important mathematical limitations

The browser verifies the **algebraic matrices** and elementary crossing arithmetic exactly. It does **not** certify isotopy classes, minimal arc intersections, the proper-product polygon exclusions, or the existence of auxiliary loops. Those are arguments described in the walkthrough and must be evaluated mathematically.

It is also **not** a counterexample to the faithfulness of the generic Burau representation: the example's matrix at `t=2` is nontrivial. The claim is limited to the intermediate Proposition 6.7 as analyzed in the conversation.

Paper: https://arxiv.org/abs/2607.05283
