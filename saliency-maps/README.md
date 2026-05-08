# Saliency Maps for Neural Networks
### A hands-on Jupyter notebook project for students learning interpretable deep learning

---

## What this project covers

**Saliency maps** answer one question: *"Which pixels in this image caused the neural network to make this prediction?"*

This project walks through that question from scratch — building a convolutional neural network, training it on MNIST handwritten digits, and then applying two techniques to visualise what it has learned:

| Method | Key idea |
|---|---|
| **Vanilla Gradient** | The gradient of the predicted class score with respect to each input pixel |
| **Grad-CAM** | A heatmap derived from the gradients and activations of the last convolutional layer |

The project also covers the **limitations** every researcher must understand before trusting saliency maps.

---

## Project structure

```
saliency-maps/
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
├── README.md
└── notebooks/
    ├── 00_prepare_dataset.ipynb   ← Run this first
    └── 01_saliency_maps.ipynb     ← Main notebook
```

**Run notebook 00 first.** It downloads MNIST, explores the data, and saves a clean
subset (`mnist_subset.npz`) used by notebook 01.

---

## How to run

### Prerequisites
- [Docker Desktop](https://www.docker.com/products/docker-desktop/) installed and running
- ~3 GB free disk space (PyTorch image)

### Start the container

```bash
cd saliency-maps
docker-compose up --build
```

The first build takes ~5–10 minutes (downloading PyTorch).
Subsequent starts take seconds.

### Open Jupyter

Navigate to **http://localhost:8890** in your browser.

Open `00_prepare_dataset.ipynb` first, run all cells, then open `01_saliency_maps.ipynb`.

### Stop the container

```bash
docker-compose down
```

---

## Notebook contents

### 00 — Prepare Dataset (12 cells)
1. Download MNIST via `torchvision` (requires internet on first run)
2. Explore class distribution and sample images
3. Compute pixel statistics (mean / std for normalisation)
4. Save a stratified subset of 6,000 train + 1,000 test images → `mnist_subset.npz`

### 01 — Saliency Maps (55+ cells)
1. Setup & motivation
2. Load dataset
3. CNN architecture walkthrough
4. Training loop (2 epochs, ~3 min on CPU)
5. Evaluation (confusion matrix, per-class accuracy)
6. **Theory** — what is a gradient-based saliency map?
7. **Vanilla Gradient** — implementation from scratch + visualisations
8. **Theory** — Grad-CAM intuition and maths
9. **Grad-CAM** — implementation from scratch (no external libraries) + visualisations
10. **Side-by-side comparison** across digits and classes
11. **Adversarial perturbation demo** — shows saliency maps can mislead
12. **Limitations** — 6 failure modes with demonstrations
13. **Exercises** — 4 hands-on challenges
14. Conclusion & further reading

---

## Technical details

| Item | Detail |
|---|---|
| Framework | PyTorch 2.4 (CPU) |
| Dataset | MNIST — 60,000 train / 10,000 test, 28×28 grayscale |
| Model | 2-layer CNN → 2 FC layers (~93% test accuracy) |
| Saliency methods | Vanilla Gradient, Grad-CAM |
| Python | 3.11 |

---

## Key concepts

**Vanilla Gradient:** For a given input image $x$ and predicted class $c$,
compute $\frac{\partial S_c}{\partial x}$ and visualise its absolute value as a heatmap.
High values = pixels that, if slightly changed, would most affect the prediction.

**Grad-CAM:** Uses the gradients of the class score with respect to the feature maps
of the last convolutional layer, then weights those feature maps by their global average gradient.
Produces a coarse but spatially meaningful heatmap.

---

## For instructors

- Change `N_TRAIN` / `N_TEST` in notebook 00 to make training faster or slower.
- Notebook 01 Section 11 (Adversarial demo) is a self-contained exercise — the student crafts a pixel perturbation that changes the saliency map without changing the prediction.
- The CNN weights are saved to `cnn_mnist.pt` after training so the student can reload them without retraining.
