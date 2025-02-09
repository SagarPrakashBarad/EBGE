# Estimation of Electronic Band Gap Energy From Material Properties Using Machine Learning

This repository contains the code and data for the paper titled **"Estimation of Electronic Band Gap Energy From Material Properties Using Machine Learning"**. The goal of this project is to predict the electronic band gap energy and band gap type (direct or indirect) of materials using machine learning models based on easily determinable material properties.

## Table of Contents
- [Estimation of Electronic Band Gap Energy From Material Properties Using Machine Learning](#estimation-of-electronic-band-gap-energy-from-material-properties-using-machine-learning)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Paper](#paper)
  - [Dataset](#dataset)
    - [Features:](#features)
  - [Methodology](#methodology)
    - [Machine Learning Algorithms:](#machine-learning-algorithms)
  - [Results](#results)
  - [Installation](#installation)

## Introduction
The electronic band gap energy is a critical property of materials that determines their applications in electronic and optoelectronic devices. Traditional methods for estimating band gap energy, such as Density Functional Theory (DFT), are computationally expensive and time-consuming. This project proposes a machine learning-based approach to predict the band gap energy and type using easily obtainable material properties, without the need for preliminary DFT calculations.

For more details, refer to the [arXiv paper](https://arxiv.org/pdf/2403.05119).

## Paper
The full paper is available on arXiv:
- **Title**: Estimation of Electronic Band Gap Energy From Material Properties Using Machine Learning
- **Link**: [arXiv:2403.05119](https://arxiv.org/pdf/2403.05119)

## Dataset
The dataset used in this project is sourced from the **Benchmark AFLOW Data Sets for Machine Learning**. The dataset contains 55,298 samples with 9 features, including properties such as electronegativity, group numbers, and atomic volumes. The dataset is divided into training and test sets, with 52,534 samples for training and 2,765 samples for testing.

### Features:
- `electronegativity`: Average electronegativity of the constituent atoms.
- `group_numbers`: Group numbers of the elements in the material.
- `volume_cell`: Volume of the unit cell.
- `volume_atom`: Volume per atom.
- `Natoms`: Number of atoms in the unit cell.
- ... (other features)

For more details, see the [data/README.md](data/README.md).

## Methodology
The methodology involves the following steps:
1. **Data Preprocessing**: The dataset is preprocessed by encoding categorical variables, standardizing, and normalizing the features.
2. **Clustering**: Non-metals are clustered into 5 groups using the k-means algorithm.
3. **Model Training**: Separate models are trained for band gap estimation and band gap type classification on each cluster.
4. **Evaluation**: The models are evaluated using a custom scoring metric that combines F1 scores for classification and mean absolute error (MAE) for regression.

### Machine Learning Algorithms:
- **Random Forest (RF)**
- **Gradient Boosting (GB)**
- **XGBoost (XGB)**
- **k-Means Clustering**

For more details, see the [notebooks/](notebooks/) and [scripts/](scripts/) directories.

## Results
The final model, called the **Clustered Gap Predictor (CGP)**, achieves the following performance:
- **Metal vs. Non-Metal Classification**: AUC score of 0.99.
- **Band Gap Estimation**: Weighted MAE of 0.2321 eV.
- **Band Gap Type Classification**: AUC score greater than 0.97 for all clusters.

For detailed results, see the [results/README.md](results/README.md).

## Installation
To set up the environment and install the required dependencies, run:

```bash
pip install -r requirements.txt
```