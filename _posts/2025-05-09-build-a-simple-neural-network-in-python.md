---
layout: post
title: "Build a Simple Neural Network in Python"
description: "A hands-on tutorial for building your first neural network in Python using modern libraries."
date: 2025-05-09
tags: [Python, neural networks, AI, tutorial, machine learning]
categories: [ai, tutorials, python, machine learning]
author: Tech Empire
image: /assets/images/ai1.jpg
---

# Build a Simple Neural Network in Python

Step-by-step guide to creating a basic neural network from scratch using Python.

Neural networks are the backbone of modern AI. They power image recognition, natural language processing, recommendation systems, and more. If you're new to machine learning, building your first neural network is a great way to understand the fundamentals.

In this tutorial, we'll walk you through how to create a simple feedforward neural network using Python and TensorFlow — one of the most popular machine learning libraries in the world.

---

## 🧠 What You'll Learn

- How neural networks work at a basic level
- Setting up your Python environment
- Writing and training a neural network to solve a basic problem
- Understanding activation functions, layers, and loss functions

---

## 🔧 Getting Started

Make sure you have Python 3 installed. Then install the required libraries:

```bash
pip install tensorflow numpy
```
🧩 Step 1: Prepare Your Data
We’ll use the classic XOR problem — a simple test case to prove that your neural network can learn non-linear patterns.

```python
import numpy as np

# Inputs
X = np.array([[0, 0], [0, 1], [1, 0], [1, 1]])

# Outputs (XOR logic)
y = np.array([[0], [1], [1], [0]])
```

🧱 Step 2: Build the Neural Network

```python
import tensorflow as tf
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense

model = Sequential([
    Dense(4, input_dim=2, activation='relu'),
    Dense(1, activation='sigmoid')
])

model.compile(optimizer='adam', loss='binary_crossentropy', metrics=['accuracy'])
model.fit(X, y, epochs=1000, verbose=0)
```

This neural network has:

* An input layer (2 features)

* One hidden layer with 4 neurons and ReLU activation

* An output layer with 1 neuron and sigmoid activation (for binary output)

📊 Step 3: Make Predictions

```python
predictions = model.predict(X)
print(predictions.round())
```

Expected output:

[[0.]
 [1.]
 [1.]
 [0.]]
```
The network has learned the XOR logic — success!

🚀 What’s Next?
Once you understand this basic structure, you can:

* Add more hidden layers

* Tweak activation functions and optimizers

* Apply the same logic to real-world data (like handwritten digits or sentiment analysis)

💬 Final Thoughts
Building a neural network from scratch is a powerful way to start your AI journey. As you grow more comfortable, you’ll be able to tackle more complex projects and architectures like CNNs and RNNs.

Stay tuned to Tech Empire for more tutorials that make machine learning simple, practical, and powerful.
