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
- The true TDDFT spectrum of the target system is used only for evaluation.

# Evaluation Metrics
- MSE: Mean Squared Error
- MAE: Mean Absolute Error
- R² Score: Coefficient of determination

# Cross-Validation
- Using leave-one-out cross-validation (LOOCV), each system is predicted by training the model on all other systems.
- The predicted spectrum is then compared to the real TDDFT spectrum to evaluate accuracy across the dataset.

# Visualization
- Plot of predicted vs. true UV-visible spectra using matplotlib.
- Machine learning analysis including feature correlation, cross-validation results, performance metrics (MSE, MAE, R² score) to quantify prediction accuracy, etc.
  
# Added Files
- Folder: Descriptors
  - descriptors.npy : Stores the correlation matrix between the descriptors used in the machine learning models.
  - Descritors plot : A visual matrix (figure) showing the correlations between features.

- Folder: importance
  - importance.npy : Contains the computed feature importances used to evaluate the relevance of each descriptor in the machine learning models.
  - Importance Plot : A figure displaying the importance of each feature as determined by the ML model.

- Folder: train-and-predict
  - train_and_predict.npy : A Python script that loads the dataset, trains multiple ML models, makes predictions on the UV-Vis spectrum, and evaluates performance.
  - Predicted vs Real Values Plot : A figure comparing the predicted and actual values to assess model accuracy.
  - Spectra Plot : A visual comparison between predicted and real UV-Vis spectra.

- Summary Figure : A comprehensive figure comparing the performance of the four ML models tested, evaluating their efficiency in predicting the UV-Vis absorption spectrum.
