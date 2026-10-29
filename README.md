<div align="center">

# ML Non-Convex Optimisation

Approximating global minima of non-convex benchmark functions using machine learning and evolutionary algorithms

[![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![License](https://img.shields.io/github/license/horse-3903/ml-non-convex-optimisation?style=flat-square)](LICENSE)
[![Last Commit](https://img.shields.io/github/last-commit/horse-3903/ml-non-convex-optimisation?style=flat-square)](../../commits)

</div>

---

## Overview

This research project investigates strategies for optimising highly non-convex, multimodal functions, a class of problems that defeats standard gradient-based methods due to numerous local minima. Three optimisation paradigms are compared: gradient descent, Bayesian optimisation, and evolutionary algorithms (differential evolution). The benchmark suite includes the Rosenbrock, Rastrigin, and Ackley functions, all of which are canonical non-convex test cases in the optimisation literature.

---

## Features

- **Three Optimisation Strategies**: Gradient descent, Bayesian optimisation, and differential evolution implemented and benchmarked side-by-side
- **Standard Benchmark Functions**: Rosenbrock, Rastrigin, and Ackley functions with known global minima for ground-truth comparison
- **Quantitative Results Logging**: Optimised values and coordinates saved as JSON for reproducibility and analysis
- **Modular Architecture**: Each optimiser and function is independently importable for extension

---

## Tech Stack

[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)](https://pytorch.org/)
[![SciPy](https://img.shields.io/badge/SciPy-8CAAE6?style=for-the-badge&logo=scipy&logoColor=white)](https://scipy.org/)

---

## Getting Started

### Prerequisites

- Python 3.8+
- Dependencies listed in `requirements.txt`

### Installation

```bash
git clone https://github.com/horse-3903/ml-non-convex-optimisation.git
cd ml-non-convex-optimisation
pip install -r requirements.txt
```

### Usage

Run each optimisation strategy independently:

```bash
# Evolutionary algorithm (differential evolution)
python src/optimise/evolutionary_optimisation.py

# Bayesian optimisation
python src/optimise/bayesian_optimisation.py

# Gradient descent
python src/optimise/gradient_descent.py
```

Results are saved to `results/<method>/<timestamp>.json`.

---

## Methodology

### Problem Statement

Non-convex functions have multiple local minima, making it trivially easy for gradient-based methods to get trapped. This project evaluates how well alternative paradigms escape local minima and converge to the true global minimum.

### Benchmark Functions

| Function | Search Space | Global Minimum |
|---|---|---|
| **Rosenbrock** | `[-5, 5]²` | `f(1, 1) = 0` |
| **Rastrigin** | `[-5, 5]²` | `f(0, 0) = 0` |
| **Ackley** | `[-5, 5]²` | `f(0, 0) = 0` |

### Optimisation Methods

1. **Gradient Descent**: Standard first-order method using PyTorch autograd; serves as a baseline and illustrates the local-minimum problem.
2. **Bayesian Optimisation**: Surrogate model-based approach that builds a probabilistic model of the objective and uses an acquisition function (e.g., Expected Improvement) to select the next query point.
3. **Evolutionary Algorithm (Differential Evolution)**: Population-based stochastic method from `scipy.optimize.differential_evolution` that evolves candidate solutions using mutation, crossover, and selection without gradient information.

### Pipeline

```
Define benchmark function + bounds
        ↓
  Run optimiser (gradient / Bayesian / evolutionary)
        ↓
  Compare optimised (x*, f*) against known global minimum
        ↓
  Log results to results/<method>/<timestamp>.json
```

---

## Results

Optimisation results are stored in the `results/` directory, organised by method. Each JSON file records:
- The optimised coordinate `x*`
- The optimised function value `f(x*)`
- The true minimum for comparison

Evolutionary algorithms consistently locate global minima on all three benchmark functions; gradient descent reliably fails on Rastrigin and Ackley due to their high density of local minima.

---

## Project Structure

```
ml-non-convex-optimisation/
├── src/
│   ├── model/              # Model training utilities
│   ├── optimise/
│   │   ├── bayesian_optimisation.py
│   │   ├── evolutionary_optimisation.py
│   │   └── gradient_descent.py
│   └── util/               # Benchmark function definitions
├── results/                # Saved optimisation results (JSON)
└── requirements.txt
```

---

## License

This project is licensed under the [MIT License](LICENSE).
