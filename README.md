# Population PK/PD Modeling of an Oral Small Molecule Drug

This project is a complete pharmacometrics workflow built in Python, covering the analysis steps that would normally be carried out in NONMEM, Monolix, or nlmixr2: study data simulation, exploratory analysis, non-compartmental analysis, structural population pharmacokinetic model development, covariate evaluation, model qualification, PK/PD linkage, and simulation-based dose selection.

## Background

The population estimation step is implemented as a Standard Two-Stage (STS) analysis: individual subject parameters are estimated by nonlinear least squares, and the population typical values and between-subject variability (omega) are derived from the distribution of those individual estimates. This is a long established pharmacometric method and produces results directly comparable to a nonlinear mixed effects model such as those fit in NONMEM, Monolix, or nlmixr2, though those platforms additionally allow simultaneous first order conditional estimation (FOCE) or stochastic approximation expectation maximization (SAEM) with shrinkage diagnostics.

## Contents

- `notebooks/pkpd_modeling_project.ipynb`: the full analysis notebook
- `data/`: simulated and derived datasets produced by the notebook
- `figures/`: figures produced by the notebook

## Data files

| File | Description |
|---|---|
| `simulated_pk_data.csv` | Raw simulated concentration-time data, 40 subjects, single 100 mg oral dose |
| `true_individual_parameters.csv` | True individual CL, V, ka values used to generate the data (for validation) |
| `individual_parameter_estimates.csv` | Individual PK parameter estimates from the Standard Two-Stage fit |
| `nca_summary.csv` | Non-compartmental analysis results per subject (Cmax, Tmax, AUC, half-life) |
| `simulated_pkpd_effect_data.csv` | Simulated concentration and pharmacodynamic effect data |
| `dose_selection_summary.csv` | Steady-state trough concentration summary for candidate once daily doses |

## Analysis steps

1. Study design and data simulation (one compartment oral absorption model with allometric covariates)
2. Exploratory analysis of concentration-time data
3. Non-compartmental analysis
4. Structural population PK model definition
5. Individual parameter estimation and population parameter derivation (Standard Two-Stage)
6. Covariate model evaluation (body weight on clearance and volume)
7. Model qualification: goodness-of-fit plots and visual predictive check
8. PK/PD model: concentration-effect relationship using an Emax model
9. Simulation-based dose selection across candidate dosing regimens
10. Summary of findings

## Running the notebook

```
pip install numpy pandas scipy matplotlib jupyter
jupyter notebook notebooks/pkpd_modeling_project.ipynb
```

## Notes on extending this work

This notebook uses a Standard Two-Stage estimation approach so that the full workflow runs in pure Python without external software dependencies. The same structural model and dataset could be re-fit in nlmixr2 (R) using FOCE or SAEM to obtain a full nonlinear mixed effects estimation with shrinkage diagnostics, which would be the natural next step when moving from an exploratory Python-based analysis to a regulatory-style pharmacometric report.
