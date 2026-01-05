This repository contains a novel molecular featurization and modeling pipeline for predicting molecular properties on the QM7 dataset. The core contribution is a Weighted Views featurization that preserves 3D geometry and chirality.



# Project Overview

Traditional molecular featurization methods often lose important geometric or chiral information. This project addresses that limitation by:
- Constructing Weighted Views of molecules based on Cartesian coordinates and interatomic distances
- Preserving chirality and spatial structure
- Extending the base featurization with single and pair properties


## Repository Structure

```text
qm7-featurization/
├── src/
│   ├── qm7_weightedviews.py        # Core Weighted Views featurization
│   ├── qm7_atom_encoder.py         # Options to add single atom properties
│   ├── qm7_pair_information.py     # Switches to add pairwise information
│   └── __init__.py
│
├── notebooks/
│   ├── qm7_full_split.ipynb        # Neural network baseline experiments
│   ├── qm7_coulomb.ipynb           # Coulomb matrix inclusion (optional)
│   └── qm7_transformer.ipynb       # Transformer based experiments
│
├── data/
│   ├── qm7_raw/                    # Original QM7 data
│
└── README.md

```

## Folder Description

The project includes several Python scripts and Jupyter notebooks for data processing, model implementation, and analysis:

## src

- qm7_weightedviews.py: This file contains the core idea and implementation of novel molecule featurization method.
- qm7_atom_encoder.py: This file contains options to add single atom properties into existing views.
- qm7_pair_information: This file contains options to add pair information between atoms e.g., Coulomb interaction. 


## notebooks

- qm7_full_split.ipynb: This notebook contains analysis on QM7 data using Neural networks only. It includes various switches to choose the origin i.e. carbon as origin, hydrogen not as origin, heavy atom as origin etc.
- qm7_coulomb.ipynb: This notebook contains experiemnts that incorporate both single atom and pairwise information. It produced better empirical results compared to qm7_full_split.ipynb.
- qm7_transformer.ipynb: This notebook contains experiments where a transformer layer is integrated into the existing prediction pipeline.


## Results

The table below presents the performance of the Transformer Encoder across various hyperparameter configurations, evaluated using Mean Absolute Error (MAE) on training and test sets:

| $d_k$ | $d_v$ | $d_q$ | $d_{ff}$ | Base Layer | End Layer | Num Blocks | Train MAE | Test MAE |
|-------|-------|-------|-----------|------------|-----------|------------|-----------|----------|
| 32    | 16    | 32    | 64        | 1          | 1         | 3          | 1.67      | 2.01     |
| 32    | 16    | 32    | 64        | 3          | 1         | 3          | 1.79      | 2.31     |
| 32    | 16    | 32    | 64        | 2          | 1         | 3          | 1.90      | 2.32     |
| 32    | 16    | 32    | 64        | 4          | 2         | 3          | 2.14      | 2.9      |
| 32    | 16    | 32    | 64        | 1          | 2         | 3          | 2.51      | 3.4      |




