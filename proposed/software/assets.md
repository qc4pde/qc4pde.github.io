# QC4PDE Software & Tooling: Assets, Work in Progress & Next Steps

*2026-11-19*


## Assets

### Repos

- QC4PDE Git Org: <https://github.com/qc4pde>
    - One repo - the web site (splash, workshop, meeting calendar, lots of
      links)
        - source: <https://github.com/qc4pde/qc4pde.github.io>
        - web: <https://qc4pde.github.io/>
        - proposed: <https://qc4pde.github.io/proposed/>

- Q8020-CFD Org: <https://github.com/Q8020-CFD>
    - many repos:
      [FVM Euler](https://github.com/Q8020-CFD/fvm_euler_1d_solver),
      [Cole-Hopf & QLBM](https://github.com/Q8020-CFD/q8020-cfd-ch-lbm),
      ports of [HHL](https://github.com/Q8020-CFD/quantum_linear_solvers),
      [SQLS](https://github.com/Q8020-CFD/sqls), etc.
    - experiment repo:
      <https://github.com/Q8020-CFD/q8020-cfd-experiments> - or link to
      other results in their home locations - towards a catalog, not a
      mono-repo
    - experiment aux: sweep definitions, analysis, post-proc code, figures,
      etc. - same concept as the experiment repo, a default location:
      <https://github.com/Q8020-CFD/q8020-cfd-experiments-aux>

### metautil

<https://github.com/Q8020-CFD/q8020-cfd-metautil>

- Python lib for common arg handling (e.g. IBM backend args)
- common metadata capture (e.g. backend calibration)
- a convenience mechanism, not a required tool - it would be common to use
  LLMs to harvest metadata from the output debris of closed-box codes
- a loose metadata spec permits eager gathering and fix-it-later
  normalization
- metadata categories:
    - *experiment* - run identification
    - *case* - problem definition (e.g. matrix, RHS, dimension)
    - *code* - algorithm, environment, library versions
    - *backend* - execution target, simulator or hardware (e.g. calibration)
    - *artifacts* - circuit details, transpilation, file inventory
    - *exec_stats* - timing, exit code, success flag
    - *results* - solution vectors, per-iteration data
    - *analysis* - fidelity, error norms, quality metrics
- the sweeper tool gives a declarative experiment definition with case arg
  expansion - again a convenience, not a requirement

### solverfwq (work in progress)

<https://github.com/Q8020-CFD/solver-fwq>

- modeled after a classical tool - [petsc4py](https://petsc.org/release/petsc4py/)
- pre-, solve, post- with numerous variations, plugins classical or quantum
- abstracted backends, perhaps using OpenQSE or other
- distributed heterogeneous workflows with results provenance - we have a
  reference architecture ([lwfm](https://github.com/lwfm-proj/lwfm)) but
  prefer to piggyback on existing workflow tools
- LLM-driven maintenance of the plugin library (using swe-pod, or a similar
  structured coding process)


## Next Steps

- general pre-release tidy-up of the above algorithm & tool assets;
  incorporate other component sets (e.g. Brightskies)
- experiment results catalog: structure, linking, maintenance plan - for
  handoff to the [Benchmarks & Stewardship](../benchmarks/README.md)
  committee
- solverfwq (with Brightskies, others?)
