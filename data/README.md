
## Dataset Overview

The dataset contains **55,298 samples** of materials, each described by **9 features**. The dataset is divided into a **training set** (52,534 samples) and a **test set** (2,765 samples). The target variables are:
- **Band Gap Energy**: A continuous value representing the energy gap between the valence and conduction bands.
- **Band Gap Type**: A categorical variable indicating whether the band gap is **direct** or **indirect**.
- **Material Type**: A binary variable indicating whether the material is a **metal** or **non-metal**.

### Features

The following features are used in the dataset:

1. **electronegativity**: The average electronegativity of the constituent atoms, calculated using the Pauling scale. Electronegativity differences between atoms influence the band gap energy.
2. **group_numbers**: The group numbers of the elements in the material, derived from the periodic table. Group numbers provide information about the electronic configuration of the material.
3. **volume_cell**: The volume of the unit cell. Smaller cell volumes tend to result in higher band gaps due to increased electron confinement.
4. **volume_atom**: The volume per atom. Similar to `volume_cell`, this feature affects electron confinement and band gap energy.
5. **Natoms**: The number of atoms in the unit cell. This feature influences the density of states, which in turn affects the band gap energy.
6. **atomic_mass**: The average atomic mass of the constituent atoms.
7. **atomic_radius**: The average atomic radius of the constituent atoms.
8. **density**: The density of the material.
9. **stoichiometry**: The stoichiometric formula of the material, encoded as numerical values.

### Target Variables

1. **Band Gap Energy**: A continuous variable representing the energy difference between the valence and conduction bands (in electron volts, eV).
2. **Band Gap Type**: A categorical variable with two classes:
   - **Direct Band Gap**: The minima of the conduction band and the maxima of the valence band are aligned in momentum space.
   - **Indirect Band Gap**: The minima of the conduction band and the maxima of the valence band are not aligned in momentum space.
3. **Material Type**: A binary variable indicating whether the material is a **metal** (band gap = 0) or a **non-metal** (band gap > 0).

### Dataset Statistics

- **Total Samples**: 55,298
  - **Training Set**: 52,534 samples
    - **Metals**: 27,396
    - **Non-Metals**: 25,138
      - **Indirect Band Gap**: 15,838
      - **Direct Band Gap**: 9,300
  - **Test Set**: 2,765 samples
    - **Metals**: 1,446
    - **Non-Metals**: 1,319
      - **Indirect Band Gap**: 843
      - **Direct Band Gap**: 476

- **Band Gap Energy**:
  - **Maximum Value**: 9.084 eV
  - **Average Value**: 1.3176 eV
  - **Standard Deviation**: 1.8079 eV

## Data Preprocessing

The raw dataset has been preprocessed to make it suitable for machine learning models. The preprocessing steps include:

1. **Encoding Categorical Variables**: The `stoichiometry` column and `group_numbers` were encoded into numerical arrays while preserving their order.
2. **Standardization and Normalization**: All features were standardized and normalized to ensure that they have a similar range and distribution, which improves the performance of machine learning models.
3. **Feature Engineering**: Two new features were engineered:
   - **electronegativity**: Calculated as the average electronegativity of the constituent atoms.
   - **group_numbers**: Derived by replacing elements in the `species` column with their corresponding group numbers from the periodic table.

## Files in This Directory

### **raw/**: Contains the original dataset files downloaded from the source.
This directory holds the raw dataset files as they were initially downloaded, along with intermediate versions of the dataset after each preprocessing step. The files are as follows:

1. **`aflow_cleaned.csv`**:
   - This file contains the dataset after initial cleaning, standardization, and normalization.
   - **Cleaning Steps**:
     - Removal of missing or invalid entries.
     - Standardization of numerical features (e.g., scaling to zero mean and unit variance).
     - Normalization of feature values to ensure consistent ranges.
   - **Purpose**: This file serves as the foundation for further preprocessing steps.

2. **`aflow_cleaned_and_encoded.csv`**:
   - This file builds upon `aflow_cleaned.csv` by adding encoding for categorical variables, specifically the stoichiometric data.
   - **Encoding Steps**:
     - The `stoichiometry` column is encoded into numerical arrays while preserving the order of elements.
     - The `group_numbers` feature is derived by replacing elements in the `species` column with their corresponding group numbers from the periodic table.
   - **Purpose**: This file is used for feature engineering and preparing the dataset for machine learning models.

3. **`aflow_cleaned_and_encoded_with_cluster_labels.csv`**:
   - This file extends `aflow_cleaned_and_encoded.csv` by adding cluster labels to the data points.
   - **Clustering Steps**:
     - Non-metals are clustered into 5 groups using the **k-means clustering algorithm**.
     - Each non-metal sample is assigned a cluster label (0 to 4) based on its properties.
   - **Purpose**: This file is used for training cluster-specific models for band gap estimation and band gap type classification.

---

### **processed/**: Contains the cleaned and preprocessed dataset files ready for model training.
This directory contains the final versions of the dataset, split into training and test sets, and fully preprocessed for machine learning tasks. The files are as follows:

1. **`aflow_training_set_with_cluster_label.csv`**:
   - This file contains the **training set** with 52,534 samples.
   - **Contents**:
     - All 9 features (e.g., `electronegativity`, `volume_cell`, `group_numbers`, etc.).
     - Target variables: `band_gap_energy`, `band_gap_type`, and `material_type`.
     - Cluster labels for non-metals (0 to 4).
   - **Purpose**: This file is used to train the machine learning models, including the metal/non-metal classifier, band gap regressor, and band gap type classifier.

2. **`aflow_test_set.csv`**:
   - This file contains the **test set** with 2,765 samples.
   - **Contents**:
     - All 9 features (same as the training set).
     - Target variables: `band_gap_energy`, `band_gap_type`, and `material_type`.
     - Cluster labels for non-metals (0 to 4).
   - **Purpose**: This file is used to evaluate the performance of the trained models on unseen data.

---

### Summary of File Usage

| File Name                                      | Purpose                                                                 |
|------------------------------------------------|-------------------------------------------------------------------------|
| `aflow_cleaned.csv`                            | Initial cleaned and standardized dataset.                               |
| `aflow_cleaned_and_encoded.csv`                | Dataset with encoded stoichiometric and group number features.          |
| `aflow_cleaned_and_encoded_with_cluster_labels.csv` | Dataset with cluster labels for non-metals.                     |
| `aflow_training_set_with_cluster_label.csv`    | Final training set with cluster labels for model training.              |
| `aflow_test_set.csv`                           | Final test set for evaluating model performance.                        |

---

### How to Use These Files

To load the preprocessed dataset in Python:

```python
import pandas as pd

# Load the training and test datasets
train_data = pd.read_csv('data/processed/aflow_training_set_with_cluster_label.csv')
test_data = pd.read_csv('data/processed/aflow_test_set.csv')

# Display the first few rows of the training set
print(train_data.head())
```