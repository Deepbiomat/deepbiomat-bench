# deepbiomat-bench

> **P3 of 4.** Combine P1's reproduced model with P2's features on a novel prediction task. Submit to a public benchmark (Matbench) or define a new one. Pair with an arXiv/Zenodo preprint.

**Status:** `v0.0.4` (pre-scaffold; repo renamed to `deepbiomat-bench` for trademark hygiene — see [`CHANGELOG.md`](./CHANGELOG.md))
**Repo path:** [`deepbiomat/deepbiomat-bench`](https://github.com/deepbiomat/deepbiomat-bench) (when created)
**License:** `MIT` for code + `CC-BY-4.0` for the preprint manuscript (locked 2026-04-21 — drag-free forkability for benchmark reproducibility; standard for preprints).
**Stack:** Python (latest stable), `uv`, P1's model package, P2's features package, `scikit-learn`, PyTorch (latest stable).

---

## Goal

Produce a single citable result that demonstrates competence at synthesis — combining reproduced methods with original features on a non-trivial task. The deliverable is a paired artifact:

1. **Benchmark code** — fully reproducible, leaderboard-ready.
2. **Preprint** — a 4–8 page paper on arXiv (`cond-mat.mtrl-sci` or `q-bio.QM`) and Zenodo, describing setup, results, and honest analysis of failure modes.

## Two Entry Modes

Choose at `v0.1.0`:

- **Mode A — Existing benchmark:** submit to an established leaderboard (e.g., Matbench). Lower bar to publish, comparable results, immediate peer signal.
- **Mode B — New task:** define a novel biomaterials prediction task that doesn't yet have a public benchmark. Higher bar, but the task definition itself becomes a community asset.

Mode A is recommended unless P1 + P2 jointly point at an obvious untapped task.

## Non-Goals

- **Not** state-of-the-art chasing — honest results > tuned numbers.
- **Not** a kitchen-sink ablation paper — one main claim, defensible.
- **Not** journal submission — preprint is the deliverable. Journal is optional, post-`v1.0.0`.
- **Not** a library (P4 handles productization).

## What Counts as Success

- Benchmark runs end-to-end from a clean clone with a single command.
- Preprint posted on arXiv + Zenodo with mintable DOI.
- Results table includes mean ± std across ≥ 5 seeds.
- All claims in the abstract are traceable to a numeric result in the repo.
- An honest "Limitations" section that names what would invalidate the conclusion.

## Methodological Standards

- **Pre-registration mindset:** define the metric and the success criterion BEFORE seeing test-set results. Document in `docs/preregistration.md` at `v0.1.0`.
- **No test-set leakage:** test set touched exactly once, after model selection.
- **Hyperparameter budget:** declared up front, reported in paper.
- **Compute budget:** declared up front, reported in paper.
- **Negative results published:** if P2's features don't help, that goes in the paper.
- **Uncertainty quantification:** every reported predictive metric paired with a calibrated uncertainty estimate (conformal, Bayesian, or empirical bootstrap); calibration verified empirically and reported. *(added in v0.0.1)*

## Versioning

- `v0.1.0` — scaffold + mode locked + pre-registration committed
- `v0.2.0` — baseline (without P2 features) running
- `v0.3.0` — P2 features integrated, full sweep running
- `v0.4.0` — full results table, sensitivity analyses
- `v0.5.0` — preprint draft circulated for self-review (against pre-registration)
- `v1.0.0` — preprint posted, DOI minted, leaderboard submission accepted (Mode A) or task definition published (Mode B)

## Prerequisites

- P1 ≥ `v1.0.0` (reproduction complete)
- P2 ≥ `v0.5.0` (features published)
- Curriculum L3 ≥ `v0.4.0`, L4 ≥ `v0.3.0` (helpful for clinical framing if Mode B)

## How to Cite

Will be added at `v1.0.0` with arXiv ID + Zenodo DOI.
