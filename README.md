# Prediction of UV-Visible Spectra from GPAW Data using Machine Learning
# Project Description

This project aims to predict the UV-visible absorption spectrum of molecular-plasmonic systems using machine learning techniques.
Our database contains 130 systems, for which full TDDFT simulations are available. However, to simulate a realistic prediction scenario, we treat each system in turn as a target with unknown spectrum, and predict its UV-visible absorption spectrum using the remaining systems as training data.
The machine learning models are trained using ground-state descriptors extracted from GPAW calculations (e.g., HOMO/LUMO levels, Fermi energy, number of electrons, geometric descriptors, PDOS, etc.).
The predicted spectrum is then compared to the true TDDFT results to assess model performance.
For more information about the systems and their design, check our publication:
**DOI: 10.1039/D4NR01198H**

# Data
Source: GPAW simulation outputs (ground state .gpw, unoccupied .gpw, and TDDFT .gpw)
Each entry includes:
- Systems ID
- Geometry-based & Physical descriptors (HOMO, LUMO, gap, number of electrons, etc.)
- PDOS spectra.
- TDDFT Uv-Vis spectrua.

# Objective
Predict the UV-visible spectrum of a target system using its ground-state properties only, without any TDDFT features.

# ML Models Used
We evaluate and compare the following regression models:

- Linear Regression
- Random Forest Regressor
- K-Nearest Neighbors (KNN)
- XGBoost Regressor

# Training Strategy
- For each target system:
  - Training data: all systems except the target system.
  - Test data: the target system, for which we simulate the prediction of its UV spectrum.
-The true TDDFT spectrum of the target system is used only for evaluation.

# Evaluation Metrics
MSE: Mean Squared Error
MAE: Mean Absolute Error
R² Score: Coefficient of determination

# Cross-Validation
Using leave-one-out cross-validation (LOOCV), each system is predicted by training the model on all other systems.
The predicted spectrum is then compared to the real TDDFT spectrum to evaluate accuracy across the dataset.

# Visualization
We compare predicted vs. true UV-visible spectrum using matplotlib.

# Added Files
- extract_features.npy: Script to extract descriptors and generate the CSV dataset.
- train_and_predict.npy: Script that loads the dataset, trains ML models, predicts the target spectrum, and evaluates performance.
- An example dataset for one system is included to demonstrate format and usage.
