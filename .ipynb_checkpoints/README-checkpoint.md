# Project Overview

This project implements a customized weighted view pipeline incorporating a Transformer Encoder for molecular property prediction using the QM7 dataset. The pipeline processes molecular data through atomic embeddings, weights, and a transformer-based architecture to generate predictions.
# Algorithms

This section presents the key algorithm used in the pipeline. Additional algorithms will be published upon the release of the associated thesis.

Transformer-Enhanced Weighted Views

The following algorithm describes the process of generating molecular property predictions using weighted views and a Transformer Encoder:

Algorithm: Transformer-Enhanced Weighted Views
Input: 
  - Views V = {V_1, ..., V_n}
  - Weights W = {w_1, ..., w_n} in ℝ^n
  - Number of encoder blocks L
  - Transformer block Block_θ: ℝ^* → ℝ^*
  - View-embedding MLP f_θ: ℝ^* → ℝ^d
  - Final MLP g_φ: ℝ^d → ℝ
Output: Predicted property ŷ in ℝ

1. Initialize z_mol ← 0 in ℝ^d <br>
2. For i = 1 to n: <br>
     a. X ← V_i  <br>
     b. For b = 1 to L: <br>
          X ← Block_θ(X)  <br>
     c. x ← flatten(X)   <br>
     d. z_i ← f_θ(x)   <br>
     e. z_mol ← z_mol + w_i * z_i  <br>
3. ŷ ← g_φ(z_mol) <br>
4. Return ŷ <br>


# Data
The data/ directory contains the QM7 dataset, stored in the qm7.mat file. This dataset includes molecular structures and properties used for training and evaluating the Transformer Encoder model.

# Notebooks and Scripts

The project includes several Python scripts and Jupyter notebooks for data processing, model implementation, and analysis:





qm7_transformercode.py: Implements the core functionality for splitting molecular views, creating a dictionary of single atom properties, calculating Coulomb matrices, and generating atomic embeddings.



qm7_weightedviews.py: Contains methods to create weighted views, with configurable switches to switch between full and truncated views.



qm7_work_full_split.ipynb: Provides analysis of full and truncated views. Requires activating the switch in qm7_weightedviews.py to generate truncated views.



qm7_coulomb_only.ipynb: Contains experiments incorporating single and pair properties in the full split configuration.



qm7_transformer_padded_zero.ipynb: Implements a customized Transformer Encoder with zero-padding for handling variable-sized inputs.

# Usage

To reproduce the results:





Ensure the QM7 dataset is available in the data/ directory.



Run the scripts or notebooks in the order described above, starting with data preprocessing (qm7_transformercode.py and qm7_weightedviews.py).



Use the notebooks for specific analyses or experiments, ensuring any required switches are set appropriately.

# Results

The table below presents the performance of the Transformer Encoder across various hyper-parameter configurations, evaluated using Mean Absolute Error (MAE) on training and test sets:

| $d_k$ | $d_v$ | $d_q$ | $d_{ff}$ | Base Layer | End Layer | Num Blocks | Train MAE | Test MAE |
|-------|-------|-------|-----------|------------|-----------|------------|-----------|----------|
| 32    | 16    | 32    | 64        | 1          | 1         | 3          | 8.69      | 9.46     |
| 32    | 16    | 32    | 64        | 3          | 1         | 3          | 9.03      | 9.89     |
| 32    | 16    | 32    | 64        | 2          | 1         | 3          | 9.20      | 10.32    |
| 32    | 16    | 32    | 64        | 4          | 2         | 3          | 12.00     | 13.13    |
| 32    | 16    | 32    | 64        | 1          | 2         | 3          | 12.41     | 13.33    |


