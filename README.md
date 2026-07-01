# Artifact for ICSE Submission

This repository provides the artifact for the submitted paper. The artifact contains the notebook-based implementation and experimental materials used to support the paper’s main claims on stage-wise fairness debugging, root-cause analysis, baseline comparison, and repair/intervention evaluation.

The artifact is anonymized for double-anonymous review.

## Repository Structure

```text
.
├── README.md
├── exp_Adult.ipynb
├── exp_Adult_mi_ablation.ipynb
├── exp_COMPAS.ipynb
├── exp_COMPAS_mi_ablation.ipynb
├── exp_German_N_Bank.ipynb
├── datasets/
│   └── [dataset files]
└── exp_result/
    ├── [generated result files]
    └── [summary tables]
```

* `*.ipynb`: Main notebook containing the implementation, experimental setup, execution code, and result generation steps.
* `datasets/`: Directory for datasets used in the experiments. Some datasets may need to be downloaded from their original public sources due to redistribution constraints.
* `exp_result/`: Directory containing generated experimental results, intermediate outputs, and summary tables.

## Overview

The artifact is designed to support independent verification of the paper’s main experimental claims. In particular, it provides materials for checking:

1. stage-wise fairness fault localization;
2. root-cause/proxy feature identification;
3. comparison with baseline methods;
4. fairness repair or intervention results;
5. reproduction of the main experimental tables reported in the paper.

The notebook is organized as an executable workflow. It includes data loading, preprocessing, model training, fairness metric computation, stage-wise debugging, root-cause analysis, baseline execution, and result summarization.

## Requirements

The artifact was tested with Python 3.10 or later.

Required Python packages include:

```text
numpy
pandas
scikit-learn
matplotlib
scipy
```

Depending on the specific experiments enabled in the notebook, the following packages may also be required:

```text
fairlearn
aif360
xgboost
```

To install the required packages, run:

```bash
pip install numpy pandas scikit-learn matplotlib scipy fairlearn aif360 xgboost
```

If running in Google Colab, most standard packages are already available. Missing packages can be installed directly in the first setup cell of the notebook.

## Datasets

The datasets should be placed under the `datasets/` directory.

Expected directory structure:

```text
datasets/
├── adult.data.csv
├── german_credit.csv
├── bank.csv
└── default_credit.csv
```

Some datasets are publicly available from external sources and are not redistributed in this repository due to licensing or redistribution considerations. For such datasets, please download the original files from the corresponding public sources and place them in the `datasets/` directory using the file names expected by the notebook.

The notebook assumes that dataset paths are defined relative to the repository root. For example:

```python
DATA_DIR = "./datasets"
RESULT_DIR = "./exp_result"
```

If the dataset file names or paths are different, update the corresponding configuration cell in the notebook before execution.

## Running the Artifact

The main artifact can be executed by opening:

```text
BiasFlow_ICSE_Artifact.ipynb
```

Then run the notebook cells sequentially from top to bottom.

The notebook is divided into the following parts:

1. environment setup and package imports;
2. dataset loading and configuration;
3. pipeline construction and preprocessing;
4. fairness metric computation;
5. stage-wise bias/fairness debugging;
6. root-cause analysis;
7. baseline comparison;
8. repair/intervention evaluation;
9. result aggregation and table generation.

Generated results will be saved under:

```text
exp_result/
```

## Quick Verification

For a lightweight check, run the notebook with the default configuration and a small number of repetitions.

Suggested quick-check setting:

```python
REPEATS = 3
TOPK_VALUES = [1, 3]
RUN_FULL_EXPERIMENTS = False
```

This quick check is intended to verify that the artifact is executable and that the main pipeline produces stage-level debugging and root-cause analysis outputs.

Expected outputs include:

```text
exp_result/stage_report.csv
exp_result/rca_result.csv
exp_result/baseline_comparison.csv
exp_result/repair_result.csv
```

The exact numeric values may slightly vary depending on package versions, random seeds, and execution environments.

## Full Reproduction

For full reproduction of the main experimental results, use the full experimental setting described in the paper.

Example setting:

```python
REPEATS = 30
TOPK_VALUES = [1, 3, 5, 10]
RUN_FULL_EXPERIMENTS = True
```

Running the full experiments may take substantially longer than the quick verification run, especially when multiple datasets, models, baselines, and repair settings are enabled.

The full run generates summary files in `exp_result/`, including stage localization results, root-cause analysis results, baseline comparison results, and repair/intervention results.

## Result Files

The `exp_result/` directory contains generated outputs such as:

```text
stage_report.csv
rca_result.csv
baseline_comparison.csv
repair_result.csv
summary_table.csv
```

These files are used to reproduce the main quantitative results reported in the paper.

A typical result file contains:

* dataset name;
* protected attribute;
* target attribute;
* injected fault type;
* detected stage;
* true fault stage;
* root-cause feature ranking;
* fairness metrics;
* accuracy or predictive performance;
* baseline comparison results;
* repair/intervention results.

## Randomness and Reproducibility

The notebook uses fixed random seeds where applicable. However, minor differences may occur across environments due to differences in package versions, model implementations, or hardware.

To improve reproducibility, please use the package versions listed in the notebook setup cell and run the cells sequentially without modifying intermediate variables.

## Notes on Anonymity

This artifact has been prepared for double-anonymous review. Author names, affiliations, acknowledgments, and other identifying information have been removed.

If the paper is accepted, we plan to release a non-anonymized archival version of the artifact with a persistent DOI.

## Troubleshooting

### Dataset file not found

Check that the dataset files are placed under the `datasets/` directory and that their names match the paths specified in the notebook.

### Missing package error

Install the missing package using:

```bash
pip install [package-name]
```

In Google Colab, run the installation command in a notebook cell before executing the remaining cells.

### Long runtime

Use the quick verification setting:

```python
REPEATS = 3
TOPK_VALUES = [1, 3]
RUN_FULL_EXPERIMENTS = False
```

Then run the full setting only after confirming that the artifact executes successfully.

## License

This artifact is provided for research review and reproducibility purposes. Dataset redistribution follows the license terms of the original dataset providers.
