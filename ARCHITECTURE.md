# Architecture: deepbiomat-bench

> Two outputs in one repo: the benchmark (code) and the preprint (manuscript). Both versioned together.

## 1. Repo Layout

```
deepbiomat-bench/
├── README.md
├── ARCHITECTURE.md
├── TODO.md
├── LICENSE                  ← MIT (code)
├── LICENSE-paper            ← CC-BY-4.0 (manuscript)
├── CHANGELOG.md
├── pyproject.toml           ← uv, depends on deepbiomat-features (P2) + deepbiomat-repro (P1) src
├── uv.lock
├── .python-version
├── Makefile
├── .pre-commit-config.yaml
├── .github/
│   └── workflows/
│       ├── ci.yml           ← lint + smoke + tests
│       ├── full-run.yml     ← manually triggered, full sweep
│       └── release.yml      ← Zenodo + arXiv submission helper
├── docs/
│   ├── preregistration.md   ← committed BEFORE seeing test results
│   ├── compute-budget.md
│   └── methods.md
├── paper/
│   ├── manuscript.tex       ← or manuscript.md → pandoc
│   ├── manuscript.bib
│   ├── figures/             ← regenerable from results/
│   └── arxiv/               ← packaged submission tarball builder
├── src/
│   └── deepbiomat_bench/
│       ├── __init__.py
│       ├── tasks.py         ← task definition (Mode B) or Matbench wrapper (Mode A)
│       ├── baselines.py     ← models without P2 features
│       ├── models.py        ← models with P2 features
│       ├── sweep.py         ← hyperparameter sweep harness
│       ├── analysis.py      ← stats, significance tests
│       └── cli.py
├── notebooks/
│   ├── 01-exploration.ipynb
│   ├── 02-baseline-results.ipynb
│   ├── 03-feature-impact.ipynb
│   └── 04-final-figures.ipynb
├── results/
│   ├── runs/                ← per-run JSON, regeneratable
│   ├── tables/              ← aggregated CSVs used in paper
│   └── checksums.txt        ← integrity for reviewers
├── tests/
└── scripts/
    ├── run_baseline.sh
    ├── run_full_sweep.sh
    └── build_paper.sh
```

## 2. Pre-Registration Workflow

```
v0.1.0 ─┬─ define task + metric + success criterion
        ├─ commit docs/preregistration.md
        ├─ tag v0.1.0  ←  immutable record
        │
v0.2.x  ├─ baseline runs (still no test-set look)
v0.3.x  ├─ feature-augmented runs (still no test-set look)
v0.4.0  └─ ONE evaluation on held-out test set
            └─ results frozen, written to results/tables/final.csv
```

Any change to pre-registration after `v0.1.0` requires a `docs/preregistration-amendments.md` entry documenting why and when. No silent edits.

## 3. Two Pipelines

### Mode A — Existing Benchmark

```
Matbench task → deepbiomat_bench.tasks.load() → P1 model → evaluate
                                          → P1 model + P2 features → evaluate
                                          → submit to Matbench leaderboard
```

### Mode B — New Task

```
Define task in src/deepbiomat_bench/tasks.py:
  ├── Dataset (from P2 if Scope B, else identified source)
  ├── Split protocol (with rationale)
  ├── Metric (with rationale)
  ├── Reference baselines (random, mean predictor, simple ML)
  └── Submission protocol (how others submit)
```

For Mode B, also publish:
- A standalone task definition in `docs/task-definition.md`
- A starter kit in `examples/` so others can submit baselines

## 4. Reproducibility (Reviewer-Friendly)

| Mechanism | Tool |
|---|---|
| Env lock | `uv.lock` committed |
| Python pin | `.python-version` |
| One-command rerun | `make all` reproduces every number in the paper |
| Result integrity | `results/checksums.txt` (SHA-256 of every results file) |
| Compute receipts | `results/runs/<id>.json` includes runtime + hardware |
| CI smoke | every PR runs `make smoke` (subset) |
| Full sweep | `full-run.yml` workflow, manually triggered, artifacts uploaded |

## 5. Paper Build

Single source of truth: either LaTeX (`paper/manuscript.tex`) or Markdown via Pandoc (`paper/manuscript.md`). Choose at `v0.1.0`. arXiv submission tarball built by `scripts/build_paper.sh`.

Figures are **never** hand-edited — every figure regenerates from `results/` via `notebooks/04-final-figures.ipynb`.

## 6. Statistics + Honesty

- Report mean ± std across ≥ 5 seeds.
- Significance tests where claims are made (paired bootstrap or Wilcoxon).
- Pre-registered metric is the headline; alternative metrics in appendix only.
- Limitations section is non-optional and reviewed against pre-registration.
- Predictive uncertainty paired with every prediction-task metric; calibration plots and miscalibration diagnostics in appendix. *(added in v0.0.1)*

## 7. Quality Gates

| Stage | Tooling |
|---|---|
| Format / Lint | `ruff format` + `ruff check` |
| Type | `pyright` strict on `src/` |
| Test | `pytest` + `pytest-cov` (≥ 80%) |
| Notebook execution | `nbmake` in CI |
| LaTeX build | `latexmk` in CI (if LaTeX) |
| Markdown lint | `markdownlint` |

## 8. Anti-Patterns to Refuse

- **Test-set tuning** — single sin that invalidates everything.
- **Cherry-picked seed** — must report distribution.
- **Headline-only honesty** — limitations get equal real estate.
- **Vendoring P1/P2** — depend on them as packages, not by copy.
- **Closed-source baselines** — every comparison must be reproducible by reviewer.
- **Unpublished compute** — readers need to know what hardware + how long.
