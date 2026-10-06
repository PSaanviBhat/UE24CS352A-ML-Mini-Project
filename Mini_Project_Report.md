# Mini-Project Report: Using Neural Network for Security Attacks Detection

**Course:** UE24CS352A- Machine Learning
**Repository:** https://github.com/PSaanviBhat/UE24CS352A-ML-Mini-Project

## Problem Statement
The objective of this project is to develop an Intrusion Detection System (IDS) capable of identifying malicious user behavior and cyber security attacks through an in-depth analysis of network traffic. Given the rapid evolution of cyber threats, the system must employ a Machine Learning approach—specifically an Artificial Neural Network (ANN)—to classify network behavior as either "Normal" or as one of four specific attack types (DoS, Probe, R2L, U2R), recognizing novel attacks not seen during training.

## Dataset Details
We utilized the **NSL-KDD dataset**, an improved version of the foundational KDD Cup 99 dataset. It contains 41 features per record (e.g., protocol type, src_bytes, num_failed_logins). 
* **Training Set:** `KDDTrain+.txt` (contains ~125,973 records)
* **Test Set:** `KDDTest+.txt` (contains ~22,544 records)

The test set is notoriously adversarial as it includes 17 new attack types (zero-day attacks) not present in the training set. The attacks were mapped into four broad categories: Denial of Service (DoS), Probing (Probe), Remote-to-Local (R2L), and User-to-Root (U2R).

## Approach and Methodology
1. **Data Preprocessing:** 
   * Categorical features (`protocol_type`, `service`, `flag`) were transformed using One-Hot Encoding, resulting in a 122-feature input matrix.
   * Numerical features were standardized to zero mean and unit variance using `StandardScaler`.
   * Labels were consolidated from over 35 specific attacks into the 5 core categories (Normal + 4 attacks) and label-encoded.
2. **Handling Class Imbalance:**
   * The training dataset is heavily imbalanced (e.g., 67,000 Normal records vs. only 52 U2R records). We mitigated this by computing **Class Weights**, forcefully penalizing the network for misclassifying rare minority classes.
3. **Model Architecture & Training:**
   * Built a Feedforward Neural Network using Keras/TensorFlow.
   * **Input:** 122 units. **Hidden Layer:** 500 units (ReLU) + 20% Dropout for regularization. **Output Layer:** 5 units (Softmax).
   * Compiled with Adam optimizer and `sparse_categorical_crossentropy` loss.
   * Trained with an **Early Stopping** callback (patience=3) to halt training the moment validation loss stagnated, restoring the optimal weights and preventing overfitting.

## Implementation Overview and Conclusions
The model was evaluated against the `KDDTest+` dataset, achieving an overall **Test Accuracy of 78.72%**. 

**Conclusions:**
* **Generalization:** This accuracy aligns precisely with benchmark expectations (~70-80%) for standard ANNs on this specific test set, demonstrating the model successfully learned underlying patterns rather than memorizing the training data.
* **Impact of Class Weights:** Our focus on handling class imbalance yielded incredible results for the rarest attack (U2R). While a baseline model achieved only 28% recall for U2R attacks, our dynamically weighted model boosted U2R recall to **70%**.
* **Final Thoughts:** While the model excels at identifying DoS attacks and Normal traffic, zero-day R2L attacks remain a challenge (12% recall) due to their similarity to normal user behavior. Future iterations could explore deep feature selection or ensemble methods. However, the current model stands as a highly robust, generalized Intrusion Detection System.
