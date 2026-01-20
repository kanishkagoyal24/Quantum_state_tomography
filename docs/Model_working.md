# Model Working
## 1. Problem Statement

The objective of this project is to reconstruct a quantum density matrix ρ from measurement data.
The reconstructed density matrix must satisfy the following physical constraints:

- Hermitian
- Positive Semi-Definite
- Unit Trace

To achieve this, a machine learning model is trained to predict a valid quantum state from simulated measurements.
## 2. Choice of Track

This project follows **Track 1: Classical Shadows**, using a Transformer-based neural network.
This choice allows flexible modeling of correlations in measurement data while keeping the system purely software-based
and suitable for rapid experimentation in Google Colab.
## 3. Model Architecture

The model consists of the following components:

- **Input Layer**: Takes flattened measurement data (real and imaginary parts).
- **Embedding Layer**: Projects inputs into a 16-dimensional feature space.
- **Transformer Encoder**:
  - 1 encoder layer
  - 2 attention heads
  - Captures correlations in measurement features
- **Output Layer**:
  - Predicts elements of a lower-triangular matrix L.
## 4. Enforcing Physical Constraints

Instead of directly predicting the density matrix ρ, the model predicts a lower-triangular matrix L.
The density matrix is reconstructed using Cholesky decomposition:

ρ = (L L†) / Tr(L L†)

This approach guarantees:

- Hermiticity: ensured by construction
- Positive Semi-Definiteness: L L† is always PSD
- Unit Trace: enforced via normalization

Thus, every output of the model is a physically valid density matrix.
## 5. Training Strategy

The model is trained using fidelity loss between the predicted and true density matrices.

## 6. Evaluation Metrics

The following metrics are used to evaluate performance:

- **Quantum Fidelity**: Measures similarity between predicted and true density matrices.
- **Trace Distance**: Measures reconstruction error.
- **Inference Latency**: Time taken to reconstruct one density matrix.
