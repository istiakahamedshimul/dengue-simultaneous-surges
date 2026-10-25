# Simultaneous dengue surges across Brazilian municipalities

Reproducible analysis code for a retrospective study of whether modeling cross-municipality dependence improves forecasts of the number of municipalities experiencing dengue surges at the same time.

The experiment analyzes weekly surveillance records from 60 municipalities in six Brazilian geographic panels during 2015–2025. Rio de Janeiro, Sao Paulo, Belo Horizonte, and Curitiba support model development; Fortaleza and Recife are reserved for geographic evaluation. Municipal surge probabilities are generated with logistic regression and gradient boosting. Independent aggregation is compared with a Gaussian shared-factor construction that preserves the same municipal marginal probabilities.

## Main finding

At the primary two-week horizon, dependence-aware logistic aggregation reduced the equally region-weighted normalized ranked probability score (RPS) from 0.024088 to 0.023173, a 3.8% point improvement. The paired difference was inconclusive: -0.000915 (95% interval -0.002119 to 0.000026). The secondary gradient-boosting comparison improved RPS by 5.7%: -0.001748 (95% interval -0.003643 to -0.000433).

Dependence changes the forecast distribution but not the expected regional count, because municipal marginal probabilities are held fixed. In the study, dependence-aware intervals widened, while hypothetical preparedness costs did not improve consistently.

## Repository contents

```text
.
|-- Dengue_Simultaneous_Surges_Full_Experiment_v2.ipynb
|-- CODE_AVAILABILITY.md
|-- CITATION.cff
|-- LICENSE
|-- README.md
|-- SHA256SUMS.txt
`-- requirements.txt
```

The notebook contains the complete workflow: data retrieval, quality checks, panel construction, model fitting, calibration, dependence estimation, probabilistic scoring, block-bootstrap uncertainty, sensitivity analyses, hypothetical reserve decisions, figures, and export of a hash manifest.

## Reproducing the analysis

### Requirements

- Python 3.11
- Internet access to the InfoDengue API
- The packages pinned in `requirements.txt`

Create an environment and launch Jupyter:

```bash
python -m venv .venv
source .venv/bin/activate  # Windows PowerShell: .venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
jupyter lab
```

Open `Dengue_Simultaneous_Surges_Full_Experiment_v2.ipynb` and run all cells from top to bottom. On a standard local run, outputs are written to `dengue_full_outputs/`; on Kaggle they are written under `/kaggle/working/`. The final cell also creates `dengue_full_results.zip`.

The workflow downloads the municipality-week inputs directly and records the request URL, retrieval timestamp, byte size, and SHA-256 digest for every downloaded file. Existing cached inputs are accepted only when their stored digest matches.

## Data source and versioning caveat

The notebook uses reported weekly dengue cases and population fields from the [InfoDengue API](https://info.dengue.mat.br/services/api). InfoDengue records are revised retrospectively. Therefore, a rerun performed later can differ from the study snapshot even when the code and random seed are unchanged. The notebook saves retrieved raw files and provenance metadata so a completed run can be archived as a fixed snapshot.

Raw surveillance data are not redistributed in this repository. They are downloaded from the source API during execution.

## Prespecified design

- Random seed: 42
- Study period: 2015–2025
- Primary horizon: two weeks
- Joint surge event: at least three municipalities surging
- Primary endpoint: equally region-weighted normalized RPS for external regions
- External geographic evaluation: Fortaleza and Recife
- Bootstrap: 1,000 calendar-block replicates with 13-week blocks

The notebook separates model fitting, calibration, dependence estimation, and evaluation chronologically. It does not replace municipalities automatically when quality gates fail.

## Interpretation

This is a retrospective revised-data analysis, not a prospective operational trial. The external evaluation contained only 13 joint-event weeks across five episodes. The reserve analysis uses generic service units and hypothetical costs; these are not observed beds, supplies, patient demand, or prevented deaths. Results should not be used directly for clinical or public-health resource allocation without prospective validation.

## Integrity

The distributed notebook SHA-256 digest is listed in `SHA256SUMS.txt`. A successful run also produces `file_hashes.csv` for generated outputs.

## License

The analysis code is released under the MIT License. Source surveillance records remain subject to the terms and attribution requirements of their original provider.

## Contact

For questions or reproducibility issues, open a GitHub issue in this repository.
