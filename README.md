# 🧠 Visualizing What CNNs Learn

### Interpreting ResNet18 using Gradient-Based Explainability

---

## 📌 Overview

This project explores **what a deep neural network actually learns internally**, using gradient-based interpretability techniques.

Instead of improving model accuracy, the focus here is:

> Understanding *why* a model makes a prediction — and *what features it relies on*

Using a pretrained **ResNet18**, the project probes the model’s internal behavior through:

* **Saliency Maps (Vanilla Gradients)**
* **Activation Maximization (Gradient Ascent)**

---

## 🎯 Core Question

Can we look inside a neural network and understand:

* What parts of an image influence its prediction?
* What the model “thinks” a class actually looks like?

---

## 🧪 Approach

### 🔹 Model

* Pretrained **ResNet18 (ImageNet)**
* No training performed
* Weights remain frozen throughout

---

### 🔹 Task 1 — Saliency Maps

Compute:

∂(class score) / ∂(input pixels)

This produces a **pixel-wise importance map** showing:

* Which regions influence the prediction most
* Where the model focuses attention

#### Key Observations:

* Strong activation along **edges and contours**
* Weak activation inside object interiors
* Some background influence
* Red & Green channels dominate (consistent with banana color)

---

### 🔹 Task 2 — Activation Maximization

Instead of analyzing a real image:

> Start from random noise and generate an image that maximizes the “banana” class score

Using gradient ascent:

```text
image = image + α × ∂(score)/∂(image)
```

---

## 🔍 What Emerges

* No clean banana shape appears
* Instead: **yellow-green textured patterns**
* Curved, repetitive structures dominate

---

## 🧠 Key Insight

> CNNs are **texture-biased**, not shape-aware

The model:

* Uses **edges** in real images
* Internally represents objects as **texture patterns**

This gap highlights a fundamental limitation of deep vision models.

---

## 📊 Experimental Evidence

### From Saliency Maps:

* Edge-focused attention
* Noisy interior gradients
* Channel-wise color sensitivity

### From Activation Maximization:

* Smooth convergence of class score
* Emergence of structured textures
* Strong RGB bias (R + G >> B)

As shown in the results:

* The banana score increases steadily from noise to a high value
* Optimization stabilizes over iterations
* Final image encodes **color + texture**, not geometry

---

## 🚀 Why This Matters

* Reveals **hidden biases in CNNs**
* Explains failure cases in real-world vision systems
* Demonstrates limitations of current architectures
* Provides intuition for **model interpretability techniques**

---

## 🛠️ Tech Stack

* PyTorch
* Torchvision (ResNet18)
* NumPy
* Matplotlib

---

## ▶️ How to Run

```bash
pip install torch torchvision matplotlib numpy
```

Then open:

```bash
pes1ug23am287-xai-3.ipynb
```

---

## ⚠️ Disclaimer

This is an **interpretability-focused experiment**, not a production model.
Results highlight model behavior, not performance optimization.

---

## 👨‍💻 Author

**Shivam Soni**  
Deep Learning | Explainable AI

---

## ⭐ Notes

This project demonstrates how:

* Backpropagation can be repurposed for **interpretability**
* Neural networks rely on **features different from human perception**
* Simple gradient methods can reveal **deep insights about model behavior**

---
