# Data-Driven Clothing for Interactive Applications

Implementation of a reduced-order machine learning model for real-time cloth simulation, based on the Stanford CS229 paper by Kangrui Xue and Jane Wu[cite: 3].

## Problem Overview
Physics-based cloth simulations produce realistic folds and wrinkles but run at around 180 seconds per frame in procedural engines, making them too slow for interactive applications[cite: 3, 6]. This project replaces the numerical solver with a neural surrogate that maps human pose angles directly to 3D garment mesh displacements in real time[cite: 3, 6].

- **Input:** 14 skeletal joint rotation quaternions (56 values total)[cite: 3].
- **Output:** 3D coordinate displacements across 2,170 vertices of a coat (6,510 values total)[cite: 3].
- **Compression:** Principal Component Analysis (PCA) reduces the 6,510 mesh displacements into a compact set of latent coefficients (64, 128, or 256) to prevent overfitting and speed up inference[cite: 4, 5].

---

## Repository Contents
- `data_driven_cloth.ipynb`: End-to-end Jupyter notebook covering data generation, PCA decomposition, model training, ablation benchmarks, and error visualization.
- `requirements.txt`: Python package dependencies.
- `README.md`: Project summary and run instructions[cite: 1].

---

## Models Tested
1. **Linear Regression (Baseline):** Direct linear mapping from 56D pose to 6,510D offsets (simulates optimal skinning).
2. **Direct MLP:** Multi-layer perceptron (`relu_128_256`) directly predicting all 6,510 vertex offsets.
3. **MLP + PCA (64, 128, 256 components):** MLP predicting latent coefficients, followed by a fixed linear PCA reconstruction layer[cite: 4, 5].

---

## How to Run

### Google Colab (Recommended)
1. Open [Google Colab](https://colab.research.google.com/).
2. Click **File > Upload notebook** and select `data_driven_cloth.ipynb`.
3. Select **Runtime > Run all**.

### Local Setup
```bash
git clone [https://github.com/](https://github.com/)satvikkalyanpur/data-driven-cloth-simulator.git
cd data-driven-cloth
pip install -r requirements.txt
jupyter notebook data_driven_cloth.ipynb
