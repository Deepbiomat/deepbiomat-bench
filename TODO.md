# TODO: deepbiomat-bench

> Atomic tasks. Open this repo only after P1 ≥ v1.0.0 and P2 ≥ v0.5.0.

**Cursor:** `v0.0.4` (gated; repo renamed to `deepbiomat-bench` for trademark hygiene — see [`CHANGELOG.md`](./CHANGELOG.md))

---

## v0.1.0 — Scaffold + Mode + Pre-Registration

- [ ] **0.1** Add LICENSE *(locked in v0.0.2: `MIT` for code, `CC-BY-4.0` for paper)*
  - [ ] 0.1.1 Add `LICENSE` file with canonical MIT text (code)
  - [ ] 0.1.2 Add `LICENSE-paper` file with canonical CC-BY-4.0 legal code (manuscript)
  - [ ] 0.1.3 SPDX headers in source files (`# SPDX-License-Identifier: MIT`)
  - [ ] 0.1.4 License footer in `paper/manuscript.{tex,md}` (CC-BY-4.0)
- [ ] **0.2** Decide mode
  - [ ] 0.2.1 Survey Matbench tasks; identify any directly relevant to P2's features
  - [ ] 0.2.2 If a strong fit exists → Mode A. If not → Mode B
  - [ ] 0.2.3 Lock decision in `docs/mode-decision.md`
- [ ] **0.3** Repo scaffold
  - [ ] 0.3.1 `pyproject.toml` (`uv`)
  - [ ] 0.3.2 `Makefile`: `setup`, `smoke`, `all`, `paper`, `lint`, `test`
  - [ ] 0.3.3 `.pre-commit-config.yaml`
  - [ ] 0.3.4 `.gitignore`, `.editorconfig`
  - [ ] 0.3.5 Source skeleton per `ARCHITECTURE.md` §1
- [ ] **0.4** Pre-registration (commit BEFORE any modeling)
  - [ ] 0.4.1 `docs/preregistration.md`: task, dataset, splits, metric, success criterion
  - [ ] 0.4.2 `docs/compute-budget.md`: max GPU-hours, max trials
  - [ ] 0.4.3 Decide hyperparameter budget; document
  - [ ] 0.4.4 Decide model classes to compare; document
  - [ ] 0.4.5 Declare UQ method up front (conformal / Bayesian / bootstrap) and target calibration metric (e.g., ECE ≤ X, prediction-interval coverage ≥ Y) *(added in v0.0.1)*
- [ ] **0.5** Paper scaffold
  - [ ] 0.5.1 Choose LaTeX or Pandoc-Markdown; decide
  - [ ] 0.5.2 Empty `paper/manuscript.{tex,md}` with section headers
  - [ ] 0.5.3 `scripts/build_paper.sh`
  - [ ] 0.5.4 `paper/manuscript.bib`
- [ ] **0.6** CI baseline (`ci.yml` only — `full-run.yml` later)
- [ ] **0.7** Tag `v0.1.0`

## v0.2.0 — Baseline Running (No P2 Features Yet)

- [ ] **1.1** Task wiring
  - [ ] 1.1.1 Mode A: integrate Matbench task loader
  - [ ] 1.1.2 Mode B: implement task per `tasks.py`
- [ ] **1.2** Baseline models in `baselines.py`
  - [ ] 1.2.1 Random predictor
  - [ ] 1.2.2 Mean / median predictor
  - [ ] 1.2.3 Simple ML (random forest or gradient boosting on raw features)
  - [ ] 1.2.4 P1's reproduced model (with stock features only)
- [ ] **1.3** Sweep harness in `sweep.py`
  - [ ] 1.3.1 Seed handling, ≥ 5 seeds per config
  - [ ] 1.3.2 Result JSON written per run
  - [ ] 1.3.3 Compute receipts (runtime, hardware)
- [ ] **1.4** Smoke test wired to CI
- [ ] **1.5** Notebook `01-exploration.ipynb` — task EDA (NO TEST SET)
- [ ] **1.6** Notebook `02-baseline-results.ipynb` — VAL set only
- [ ] **1.7** Tag `v0.2.0`

## v0.3.0 — P2 Features Integrated

- [ ] **2.1** `models.py` — P1 model + P2 features
  - [ ] 2.1.1 Featurization pipeline using `deepbiomat-features`
  - [ ] 2.1.2 Model variants (ablation: features-only, model-only, combined)
- [ ] **2.2** Full sweep on validation set
  - [ ] 2.2.1 Run within compute budget
  - [ ] 2.2.2 Persist all run JSONs
- [ ] **2.3** Notebook `03-feature-impact.ipynb` — VAL set analysis
- [ ] **2.4** Statistical analysis in `analysis.py`
  - [ ] 2.4.1 Aggregation across seeds
  - [ ] 2.4.2 Significance tests prepared (will run on test set in v0.4)
- [ ] **2.5** Tag `v0.3.0`

## v0.4.0 — Test-Set Evaluation (One-Shot)

- [ ] **3.1** Final model selection (locked from val results, no peeking ahead)
- [ ] **3.2** Test-set evaluation — run ONCE
  - [ ] 3.2.1 Execute `scripts/run_full_sweep.sh --test` exactly once
  - [ ] 3.2.2 Persist results immutably to `results/tables/final.csv`
  - [ ] 3.2.3 Generate `results/checksums.txt`
- [ ] **3.3** Significance tests
- [ ] **3.4** Uncertainty quantification *(added in v0.0.1)*
  - [ ] 3.4.1 Apply pre-registered UQ method (per §0.4.5) to all test-set predictions
  - [ ] 3.4.2 Compute calibration metrics (ECE for classification; coverage + sharpness for regression)
  - [ ] 3.4.3 Generate reliability diagrams + miscalibration plots
  - [ ] 3.4.4 Compare actual vs pre-registered calibration target
- [ ] **3.5** Sensitivity analyses *(was 3.4 in v0.0.0)*
  - [ ] 3.5.1 Hyperparameter sensitivity
  - [ ] 3.5.2 Feature ablation
  - [ ] 3.5.3 Seed variance
- [ ] **3.6** Notebook `04-final-figures.ipynb` — all paper figures regenerate *(was 3.5 in v0.0.0)*
- [ ] **3.7** Compare actual vs pre-registered success criterion *(was 3.6 in v0.0.0)*
  - [ ] 3.7.1 Document outcome honestly in `docs/preregistration.md` (append, don't edit)
- [ ] **3.8** Tag `v0.4.0` *(was 3.7 in v0.0.0)*

## v0.5.0 — Preprint Draft

- [ ] **4.1** Manuscript first pass
  - [ ] 4.1.1 Abstract (every claim traceable to `results/tables/`)
  - [ ] 4.1.2 Introduction + related work
  - [ ] 4.1.3 Methods (matches code; cross-reference modules)
  - [ ] 4.1.4 Results (figures from notebook 04)
  - [ ] 4.1.5 Discussion
  - [ ] 4.1.6 Limitations (non-trivial; review against pre-registration)
  - [ ] 4.1.7 Reproducibility statement (pointer to repo + tag)
- [ ] **4.2** Self-review pass
  - [ ] 4.2.1 Print + read once on paper or e-reader
  - [ ] 4.2.2 Verify each abstract claim against results table
  - [ ] 4.2.3 Verify pre-registration alignment
- [ ] **4.3** External read (optional but recommended)
  - [ ] 4.3.1 Send to one peer; log feedback
- [ ] **4.4** Tag `v0.5.0`

## v1.0.0 — Posted

- [ ] **5.1** Pre-publication
  - [ ] 5.1.1 `CHANGELOG.md` finalized
  - [ ] 5.1.2 README install instructions verified on fresh env
  - [ ] 5.1.3 `make all` regenerates every paper number from clean clone
- [ ] **5.2** Submission
  - [ ] 5.2.1 arXiv submission (`cond-mat.mtrl-sci` or `q-bio.QM`)
  - [ ] 5.2.2 Mode A: Matbench leaderboard submission
  - [ ] 5.2.3 Mode B: announce task in relevant community channel
- [ ] **5.3** Archival
  - [ ] 5.3.1 GitHub Release → Zenodo DOI
  - [ ] 5.3.2 README badge with arXiv ID + DOI
- [ ] **5.4** Cross-link
  - [ ] 5.4.1 Update curriculum repo's `references.bib`
  - [ ] 5.4.2 P4 README links here as the canonical demonstration of the workflow
- [ ] **5.5** Tag `v1.0.0`

---

## Backlog (Unscheduled, Post-v1.0.0)

- [ ] Journal submission (only if reviewers' feedback is genuinely useful)
- [ ] Follow-up paper extending the negative results
- [ ] Tutorial / workshop submission
- [ ] **Additive-manufacturing parameter prediction** as a follow-up benchmark task — directly aligned with one of the three exemplar domains in Basu et al. 2022 (biomaterialomics). *(added in v0.0.1)*

## Open Questions

- _populated during mode + pre-registration_
