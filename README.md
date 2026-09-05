# Thesis-project_biosignal-processing_with-ML
Machine learning pipeline for non-invasive gesture recognition using multi-channel surface EMG (sEMG) signals, including signal preprocessing, feature extraction, feature selection, and classification
# sEMG Gesture Recognition

A machine learning pipeline for non-invasive gesture recognition using multi-channel surface electromyography (sEMG) signals.

## Overview

This repository presents the implementation of an sEMG-based gesture recognition system developed as part of an undergraduate research project in Electrical & Electronic Engineering.

The project investigates whether muscle activity recorded from the forearm can be used to distinguish hand gestures without relying on camera-based input.

The complete pipeline consists of:

**sEMG Acquisition → Signal Filtering → Feature Extraction → Feature Standardization → Feature Selection → Machine Learning Classification → Performance Evaluation**

## Project Highlights

* Multi-channel surface EMG signal acquisition
* Signal preprocessing using band-pass and notch filtering
* Extraction of handcrafted features from multiple signal domains
* Feature standardization using Z-score normalization
* Feature selection using:

  * Recursive Feature Elimination (RFE)
  * Mutual Information
  * ANOVA F-Test
  * LASSO with Cross-Validation
* Comparison of multiple tree-based machine learning classifiers:

  * Extra Trees
  * Random Forest
  * XGBoost
  * LightGBM
* Evaluation using accuracy, precision, recall, and F1-score

## Dataset

The experimental dataset contains multi-channel sEMG recordings collected from human participants performing selected static hand gestures.

For the static gesture classification experiments:

* **Participants:** 10
* **Gesture classes:** 9
* **sEMG channels:** 4
* **Sampling frequency:** 2000 Hz
* **Static gesture instances:** 900
* **Recording protocol:** 3 seconds rest followed by 3 seconds of gesture activity
* **Features:** 60 features per channel
* **Total extracted features:** 240

The original participant-level dataset is not included in this repository.

## Signal Processing

The recorded sEMG signals are processed to reduce motion artifacts, power-line interference, and high-frequency noise.

The preprocessing pipeline uses:

* **Band-pass filtering:** 30–500 Hz
* **Notch filtering:** 50 Hz

The filtered signals are subsequently used for feature extraction.

## Feature Engineering

A total of 60 features are extracted from each sEMG channel, covering multiple signal characteristics.

Feature groups include:

* Time-domain features
* Frequency-domain features
* Time-frequency and wavelet features
* Nonlinear and higher-order statistical features
* Entropy and information-theoretic features
* Model-based and other features

With four channels, the complete feature representation contains **240 features**.

## Feature Selection

To reduce dimensionality and identify informative features, four feature-selection approaches are investigated:

1. Recursive Feature Elimination (RFE)
2. Mutual Information
3. ANOVA F-Test
4. LASSO with Cross-Validation

The number of selected features is evaluated systematically using 5-fold cross-validation on the training data.

## Classification

Four machine learning classifiers are evaluated:

| Model         | Selected Features | Accuracy |
| ------------- | ----------------: | -------: |
| Extra Trees   |                31 |   95.56% |
| Random Forest |                42 |   93.33% |
| LightGBM      |                40 |   92.22% |
| XGBoost       |                65 |   88.33% |

The Extra Trees classifier produced the strongest performance in the evaluated experiments, achieving **95.56% accuracy using 31 selected features**.

## Results

The experiments demonstrate that informative handcrafted sEMG features combined with feature selection can provide strong classification performance while substantially reducing the feature dimensionality.

The best-performing configuration used:

**RFE → 31 selected features → Extra Trees**

Performance:

* **Accuracy:** 95.56%
* **Precision:** 95.70%
* **Recall:** 95.56%
* **F1-score:** 95.50%

## Repository Structure

```text
src/
    preprocessing/
    features/
    selection/
    models/

notebooks/
    signal preprocessing
    feature extraction
    feature selection
    model comparison

results/
    figures/
    tables/
```

## Reproducibility

The repository contains the implementation of the signal-processing and machine-learning pipeline.

Because the recordings involve human participants, the original participant-level dataset is not publicly included. Dataset access is subject to the conditions under which the data were collected.

## Research Status

This repository is intended to document and showcase the technical implementation of the research project. The associated manuscript is currently under review.

## Authors

**Aritra Sarkar**
Department of Electrical & Electronic Engineering
Chittagong University of Engineering & Technology (CUET), Bangladesh

Contributors:

* Pritam Bol
* Fahim Mahmud
* Aditta Chowdhury

## Acknowledgment

The implementation of this project was supported by the Biomedical Engineering Laboratory at Chittagong University of Engineering & Technology.

---

*This repository focuses on the computational implementation and experimental workflow rather than reproducing the complete manuscript.*

