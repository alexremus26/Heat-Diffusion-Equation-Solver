# 2D Heat Diffusion Equation Solver

## Overview
This project implements a numerical solver for the 2D stationary heat diffusion equation on a rectangular domain. It uses the Finite Difference Method (FDM) to discretize the Partial Differential Equation (PDE) into a sparse linear system, which is then solved efficiently.

A key feature is the custom implementation of **2D quadratic spline interpolation**, built from scratch using successive 1D row and column interpolations. The coefficients for these splines are calculated using a custom QR factorization algorithm (via modified Gram-Schmidt), also implemented from scratch.

The solver is validated against an analytical solution to analyze convergence rates across different grid densities.

## Key Features
* **Finite Difference Method (FDM):** Discretizes the 2D PDE with variable diffusion coefficients into a large, sparse linear system.
* **Custom Spline Interpolation:** Implements 2D quadratic spline interpolation from scratch to reconstruct a continuous solution from discrete grid points.
* **QR Factorization from Scratch:** Solves the linear systems for spline coefficients using a custom-built QR decomposition algorithm.
* **Sparse Matrix Operations:** Utilizes `scipy.sparse` for efficient storage and solution of the large linear systems arising from FDM.
* **Error & Convergence Analysis:** Automatically compares numerical results with an analytical solution, plotting error surfaces and calculating convergence rates.

## Mathematical Model
The solver addresses the stationary heat diffusion equation:
$$- \nabla \cdot (k(x,y) \nabla u) = f(x,y)$$
on the domain $\Omega = [0, 5] \times [0, 2]$, subject to:
* **Dirichlet Boundary Conditions:** On $y=0$ and $y=2$.
* **Neumann Boundary Conditions:** On $x=0$ and $x=5$.

## Technologies Used
* **Python 3.x**
* **NumPy:** For numerical operations and dense matrix handling in the QR solver.
* **SciPy:** Specifically `scipy.sparse` and `scipy.sparse.linalg.spsolve` for handling the main FDM linear system.
* **Matplotlib:** For 3D visualization of solutions and error surfaces, and 2D convergence plots.

## How to Run
1.  Ensure you are in the root directory of the project:
    ```bash
    pip install -r requirements.txt
    ```
2.  Run the main script:
    ```bash
    python main.py
    ```
The script will sequentially solve the problem for grid sizes $N \in \{4, 8, 16, 32\}$, display 3D plots for each, and finally show a convergence graph with calculated rates.
