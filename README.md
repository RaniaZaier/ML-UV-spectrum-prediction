# Prediction of UV-Visible Spectra from GPAW Data using Machine Learning
# Project Description

This project aims to predict the UV-visible absorption spectrum of a molecular-plasmonic system using machine learning techniques.
The target system's TDDFT simulation is not available, so we rely on other systems with completed simulations to build a predictive model.
Our approach is based on supervised learning using descriptors extracted from GPAW calculations (e.g., HOMO/LUMO levels, Fermi energy, electron count, geometric descriptors, etc.), excluding any TDDFT-related features for the target system.

# Data
Source: GPAW simulation outputs (ground state .gpw, unoccupied .gpw, and TDDFT .gpw)
Stored as a CSV file: uv_database.csv
Each entry includes:

- System ID
- Physical descriptors (HOMO, LUMO, gap, number of electrons, etc.)
- Geometry-based descriptors (distance to nanoparticle, number of neighbors, etc.)
- TDDFT spectrum (peaks + intensities) — available only for training systems

# Objective
Predict the UV-visible spectrum of a target system using its ground-state properties only, without any TDDFT features.

# ML Models Used
We evaluate and compare the following regression models:

- Random Forest Regressor
- Support Vector Machine (SVR)
- K-Nearest Neighbors (KNN)
- Linear Regression
- Decision Tree Regressor
- XGBoost Regressor

# Training Strategy
- Input features: descriptors like HOMO, LUMO, gap, n_electrons, etc.
(TDDFT-related features like excitation energy or oscillator strength are excluded for the target system)

- Training data: all systems except the target system

- Test data: the target system, for which we simulate the prediction of its UV spectrum

The true TDDFT spectrum of the target system is used only for performance evaluation.

# Evaluation Metrics

MSE: Mean Squared Error
MAE: Mean Absolute Error
R² Score: Coefficient of determination

# Visualization
We compare predicted vs. true UV-visible spectrum using matplotlib.

# Added Files
- extract_features.npy: Script to extract descriptors and generate the CSV dataset.
- train_and_predict.npy: Script that loads the dataset, trains ML models, predicts the target spectrum, and evaluates performance.
- uv_database.csv: CSV dataset containing descriptors and spectra.
