# Neural Network for Security Attacks Detection

This repository contains the source code for the **UE24CS352A- Machine Learning** mini-project. The project focuses on building an Artificial Neural Network (ANN) to detect cybersecurity attacks using the NSL-KDD dataset.

## Project Structure
- `preprocessing.ipynb`: Jupyter notebook for loading the dataset, performing one-hot encoding, feature scaling, and separating features and labels. 
- `model_training.ipynb`: Jupyter notebook for defining, compiling, and training the Artificial Neural Network. It includes data loading, model compilation with class weights, early stopping, and model evaluation.

## Setup Instructions

1. **Clone the repository:**
   ```bash
   git clone https://github.com/PSaanviBhat/UE24CS352A-ML-Mini-Project.git
   cd UE24CS352A-ML-Mini-Project
   ```

2. **Download the Dataset:**
   - Download the NSL-KDD dataset (specifically `KDDTrain+.txt` and `KDDTest+.txt`).
   - Create a `data/` folder in the root directory.
   - Place the dataset files inside the `data/` folder.

3. **Install Dependencies:**
   Ensure you have a Python environment (e.g., Conda) with the following libraries installed:
   - `numpy`
   - `pandas`
   - `scikit-learn`
   - `tensorflow` (version 2.15.0 or compatible)
   - `matplotlib`
   - `seaborn`

4. **Run the Code:**
   - First, run `preprocessing.ipynb` to process the raw dataset and save the numerical arrays (`X_train.npy`, `y_train.npy`, etc.) into the `data/` folder.
   - Second, run `model_training.ipynb` to build, train, and evaluate the Neural Network model.

## Model Details
The Neural Network architecture consists of:
- An input layer matching the one-hot encoded feature count (122 features).
- A dense hidden layer with 500 neurons (ReLU activation).
- A dropout layer (20%) for regularization.
- An output layer with 5 neurons (Softmax activation) to classify traffic into one of five categories: `normal`, `dos`, `probe`, `r2l`, and `u2r`.

The model utilizes **class weights** to heavily penalize misclassifications on rare attack classes (like U2R and R2L) and incorporates an **Early Stopping** callback to prevent overfitting and restore the best model weights.

## Evaluation
The model achieves approximately **79% accuracy** on the `KDDTest+` dataset, effectively identifying novel and zero-day attacks with particularly high recall for standard attacks and significantly improved recall for U2R attacks thanks to the class weighting.
