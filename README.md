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

The dataset was acquired using a **4-channel BIOPAC MP36 data acquisition system** with surface EMG electrodes. It contains recordings of both **static and dynamic Bangla Sign Language gestures** collected from 10 participants.
<p align="center">
  <img src="biopac_mp36.jpg" alt="BIOPAC MP36 Device" width="500">
</p>

<p align="center">
  <strong>Figure 1. BIOPAC MP36 system used for EMG data acquisition.</strong>
</p>


The static gesture dataset consists of nine Bangla Sign Language vowel gestures. In addition, five commonly used Bangla Sign Language words were recorded as dynamic gestures for potential future research.

The dataset was collected as part of an academic research study on EMG-based Bangla Sign Language recognition.


---

## Experimental Setup

EMG signals were acquired at the Biomedical Laboratory of Chittagong University of Engineering and Technology (CUET), Bangladesh, using a 4-channel MP36 BIOPAC system (BIOPAC Systems, Inc., USA) with BIOPAC Student Lab (BSL) software.

SS2LB electrode lead sets with smart and simple sensor connectors were used together with disposable Ag/AgCl surface electrodes for non-invasive EMG signal acquisition.

Before electrode placement, the skin was cleaned with alcohol to remove oils and dead skin cells and to improve the quality of the recorded EMG signals.
Four forearm muscles were selected for EMG acquisition:

* Flexor Carpi Ulnaris (FCU)
* Extensor Carpi Ulnaris (ECU)
* Extensor Carpi Radialis (ECR)
* Flexor Carpi Radialis (FCR)

These muscles were selected because they contribute to important wrist movements, including flexion, extension, radial deviation, and ulnar deviation.


---

## Electrode Placement

<p align="center">
  <img src="muscle_position.jpg" alt="Electrode Placement" width="600">
</p>

<p align="center">
  <strong>Figure 2. Electrode placement over the selected forearm muscles.</strong>
</p>

The surface electrodes were placed over four forearm muscles:

| Channel   | Muscle                  | Abbreviation |
| --------- | ----------------------- | ------------ |
| Channel 1 | Flexor Carpi Ulnaris    | FCU          |
| Channel 2 | Extensor Carpi Ulnaris  | ECU          |
| Channel 3 | Extensor Carpi Radialis | ECR          |
| Channel 4 | Flexor Carpi Radialis   | FCR          |
| Ground | Wrist/Tendon region where electrical activity was expected to be minimal  | None         |

---

## Dataset Description


The dataset contains both **static and dynamic Bangla Sign Language (BdSL) gestures**.

### Static Gestures — Bangla Vowels

Nine static gestures corresponding to the nine selected **Bangla vowels** were recorded. These gestures represent the following Bangla vowel characters:

| Gesture ID | Bangla Vowel | Type   |
| ---------- | ------------ | ------ |
| Static-01  | অ            | Static |
| Static-02  | আ            | Static |
| Static-03  | ই/ঈ          | Static |
| Static-04  | উ/ঊ          | Static |
| Static-05  | ঋ            | Static |
| Static-06  | এ            | Static |
| Static-07  | ঐ            | Static |
| Static-08  | ও            | Static |
| Static-09  | ঔ            | Static |

All nine static gestures are officially included in the **Bengali Sign Language Dictionary**.

### Dynamic Gestures — Common Bangla Sign Language Words

Five commonly used words from **Bangla Sign Language (BdSL)** were also recorded as dynamic gestures. These gestures were not analyzed in the current study and were retained for potential future research.

| Gesture ID | English Meaning | Bangla Word | Type    |
| ---------- | --------------- | ----------- | ------- |
| Dynamic-01 | Fish            | মাছ         | Dynamic |
| Dynamic-02 | Chicken         | মুরগি        | Dynamic |
| Dynamic-03 | Sweet           | মিষ্টি         | Dynamic |
| Dynamic-04 | Rice            | ভাত         | Dynamic |
| Dynamic-05 | Mother          | মা           | Dynamic |

All five dynamic gestures are part of the selected Bangla Sign Language vocabulary used during data collection.

### Dataset Summary

| Category      | Number of Classes | Instances per Class | Total Instances |
| ------------- | ----------------: | ------------------: | --------------: |
| Static vowels |                 9 |                 100 |             900 |
| Dynamic words |                 5 |                 100 |             500 |
| **Total**     |            **14** |                   — |       **1,400** |

Each gesture class contains **100 recorded instances**, obtained from 10 participants with 10 repetitions per gesture.

---

## Participants

Data were collected from **10 participants**.

| Parameter              | Description                                            |
| ---------------------- | ------------------------------------------------------ |
| Number of participants | 10                                                     |
| Age range              | 20–25 years                                            |
| Participant condition  | Healthy and physically fit                             |
| Training               | Participants received prior gesture-execution training |
| EMG channels           | 4                                                      |

Participants were trained using video lessons before data collection to improve consistency in gesture execution.

All participant identities are anonymized using participant IDs.

---

## Data Acquisition Protocol

Each gesture recording followed a fixed protocol.

For each trial:

1. The participant remained in a rest position for **3 seconds**.
2. The participant performed the selected sign gesture for **3 seconds**.
3. The procedure was repeated **10 times for each gesture**.

The same procedure was followed for all selected static and dynamic gestures.

The sampling frequency was set to **2000 Hz**, which satisfies the Nyquist sampling criterion for the frequency components of the recorded EMG signals.

### Recording Parameters

| Parameter                               | Value     |
| --------------------------------------- | --------- |
| Sampling frequency                      | 2000 Hz   |
| Rest duration                           | 3 seconds |
| Gesture duration                        | 3 seconds |
| Total duration per trial                | 6 seconds |
| Repetitions per gesture per participant | 10        |
| Number of participants                  | 10        |
| EMG channels                            | 4         |

At a sampling frequency of 2000 Hz, each 3-second segment contains approximately **6000 samples**.

---

## Dataset Statistics

### Static Gestures

The dataset contains:

* 10 participants
* 9 static gesture classes
* 10 repetitions per gesture per participant

Therefore:

**10 × 9 × 10 = 900 static gesture instances**

### Dynamic Gestures

The dataset contains:

* 10 participants
* 5 dynamic gesture classes
* 10 repetitions per gesture per participant

Therefore:

**10 × 5 × 10 = 500 dynamic gesture instances**

### Total

The complete dataset contains:

**900 static + 500 dynamic = 1400 recorded instances**

Each gesture class contains **100 instances** across the 10 participants and 10 repetitions.

---

## Dataset Organization

The dataset will be organized using anonymized participant IDs and gesture labels.

A simplified structure is shown below:

```text
dataset/
│
├── Static_Gestures/
│   ├── Subject01/
        ├──ges1.xlsx/
        ├──ges2.xlsx/
        ├──....
│   ├── Subject02/
│   ├── Subject03/
│   └── ...
    
│
└── Dynamic_Gestures/
│   ├── Subject01/
        ├──dyn1.txt/
        ├──dyn2.txt/
        ├──....
│   ├── Subject02/
│   ├── Subject03/
│   └── ...
```

Each participant folder contains the recordings associated with that participant.


---

## EMG Signal Quality and Preprocessing

EMG signals are weak bioelectrical signals and can be affected by various sources of noise, including external interference and physiological artifacts.

During data acquisition, appropriate signal conditioning and filtering were applied using the BIOPAC MP36 system to improve the quality of the recorded EMG signals.

Detailed preprocessing procedures and feature-extraction methods associated with the research study will be documented separately where applicable.

---

## Data Privacy

The dataset was collected from human participants.

To protect participant privacy:

* Participant names are not included.
* Personal identifying information is not included.
* Participants are represented using anonymized IDs.
* Consent forms and other confidential documents are not included in this repository.

The public release of the dataset will be subject to the applicable research, ethical, and institutional requirements.


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

