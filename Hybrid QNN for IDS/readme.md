# **Hybrid Classical-Quantum Neural Network**

## **Overview**
This project demonstrates a hybrid classical-quantum neural network using **TensorFlow** and **PennyLane** to classify data from a **DoS Attack Dataset**. The model combines classical dense layers with a quantum circuit to leverage the power of quantum computing for enhanced classification.

---

## **Key Features**
- **Dataset**:
  - Features include packet and device metrics such as `frame.len`, `temperature`, `pitch`, etc.
  - Class labels are one-hot encoded for binary classification.
- **Quantum Circuit**:
  - **5 qubits**
  - **2 quantum layers** with parameterized gates (RX, RY, RZ).
  - Entanglement achieved using **CNOT gates**.
- **Hybrid Model**:
  - Classical layers extract features and pass them to the quantum circuit.
  - Softmax activation for final classification.

---

## **Requirements**
### **Dependencies**
Ensure the following libraries and versions are installed:

```bash
pandas==1.3.0
numpy==1.19.5
scikit-learn==0.24.2
tensorflow==2.4.0
pennylane==0.17.0
matplotlib==3.4.2
```

Install dependencies using:
```bash
pip install pandas numpy scikit-learn tensorflow pennylane matplotlib
```

---

## **Dataset**
### **Source**
The dataset `dos_data.csv` contains **1,968 samples** with a **3:1 ratio** of genuine to fraudulent samples.

### **Features**
- Packet-level metrics: `frame.len`, `wlan.duration`, etc.
- Device-level metrics: `temperature`, `battery`, `pitch`, etc.

### **Preprocessing**
Data preprocessing includes:
1. Shuffling the dataset.
2. Normalizing features using **MinMaxScaler**.
3. Splitting data into training and testing sets.
4. One-hot encoding of labels.

---

## **Model Architecture**
### **Classical Layers**
- Dense layers with **ELU activation** for feature extraction.
- Intermediate output reshaped for quantum input.

### **Quantum Circuit**
- Parameterized gates (RX, RY, RZ) for input and intermediate layers.
- Full entanglement with **CNOT gates**.
- Measurement: Expectation values of Pauli-Z operators for each qubit.

### **Hybrid Model**
Combines classical and quantum components:
```python
model = tf.keras.Sequential([
    layers.Dense(10, activation="elu"),
    layers.Dense(15, activation="elu"),
    qml.qnn.KerasLayer(quantum_nn, weight_shapes, output_dim=5),
    layers.Dense(2, activation='softmax')
])
```

---

## **Training**
### **Hyperparameters**
- Optimizer: **Adam** (learning rate = 0.1).
- Batch size: **190**.
- Epochs: **50**.

### **Training Process**
Training was conducted on a subset of **7,500 samples**, with both training and validation splits.

---

## **Results**
### **Loss Curve**
- Training and validation loss over epochs:
  ![Training and Validation Loss](./Hybrid%20QNN%20for%20IDS/Figures/loss.png)

### **Accuracy Curve**
- Training and validation accuracy over epochs:
  ![Training and Validation Accuracy](./Hybrid%20QNN%20for%20IDS/Figures/acc.png)

---

## **Code Structure**
1. **Data Preparation**: Load, preprocess, and split the dataset.
2. **Quantum Circuit**: Define the quantum circuit with parameterized gates and entanglement.
3. **Hybrid Model**: Combine classical and quantum components for classification.
4. **Training and Visualization**: Compile the model, train it, and visualize performance.

---

## **Figures**
1. **Loss Curve**:
   - Visualizes the training and validation loss over epochs.
   - Saved as `loss.png`.

2. **Accuracy Curve**:
   - Displays the training and validation accuracy.
   - Saved as `accuracy.png`.

---

## **Author**
**Atit Pokharel**  
Department of Electrical and Computer Engineering, University of Alabama in Huntsville, USA  
Email: [ap1284@uah.edu](mailto:ap1284@uah.edu)

---

## **References**
1. PennyLane Documentation: [PennyLane](https://pennylane.ai/documentation.html)
2. TensorFlow Documentation: [TensorFlow](https://www.tensorflow.org/)

---

## **Acknowledgments**
Special thanks to the Department of Electrical and Computer Engineering at UAH for resources and support.

