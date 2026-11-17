
# HT-NN RHS 2D case

## Overview
* This project implements a 2D groundwater flow model for 
**Hydraulic Tomography Neural Network (*HT-NN*)** to estimate 
spatial distribution of **hydraulic conductivity (*K*)**.

* In this study, the **River Head Stage (*RHS*)** is introduced as time-varying head boundary that act as the main stimulus to the 2D groundwatwer system. Observation wells distributed throughout the domain will then record the head response induced by the RHS boundary.

* To generate training dataset for HT-NN,a **Monte Carlo framework** is conducted. Random K fields are generated and the corresponding groundwater simulation are performed to collect the head response from each observation well.

* The result dataset contain paired random K field and simulated head, also added the original RHS to the simulated head as input, which are used to train supervised learning model for predicting K field by observing head response.


## Features
- 2D groundwater flow simulation
- Sythetic *RHS* signal generation
- Random *K* field generation
- Forward simulation using **VSAFT3**
- Training dataset generation
- Deep learning-based hydraulic tomography inversion
- Modeling training and evaluation
- Sythetic case study

## Project Structure
```text
HTNN-2D/
├── src/
├── main.ipynb
├── training.ipynb
├── sle.py
├── train.py
├── pyproject.toml
├── requirements.txt
├── uv.lock
├── README.md
└── toy_case/
    ├──  *.dat (VSAFT files)
    └──  SLE.exe
```

## Installation

This project uses `uv` for Python environment management.
Clone the repository:
```bash
git clone https://github.com/username/HTNN-2D.git
cd HTNN-2D
```
Create the virtual environment and install dependencies:
```bash
uv sync
```

## Methodology
1. Develop 2D groundwater model with RHS boundary using *VSAFT*
2. Generate random *K* fields using gstool.
3. Perform groundwater forward simulations and collecting results.
4. Generate training datasets.
5. Develop HT-NN framework
6. Training HT-NN model.
7. Evaluate hydraulic conductivity predictions using a sythetic case.

## HT-NN input and output representation
- head matrix (**H**)

$$
\mathbf{H_{input}} =
\begin{bmatrix}
h_{obs_1}(t_1) & \cdots & h_{obs_{N_w}}(t_1) & RHS(t_1)\\
\vdots & \ddots & \vdots & \vdots \\
h_{obs_1}(t_{N_t}) & \cdots & h_{obs_{N_w}}(t_{N_t})& RHS(N_t)
\end{bmatrix}
$$

- Input (**X**) dimension:  

$$
\mathbf{X} \in \mathbb{R}^{B \times C_{in}\times N_t \times (N_w+1)}
$$

- $RHS$: River Head Stage original signal.
- $N_w$: Number of observation wells.
- $N_t$: Number of observation time steps.
- $C_{in}$ : Input channel number (Depend the parameters you want to estimate).
- $B$    : Batch Size.

- Random field matrix (**K**)

$$
\mathbf{K} =
\begin{bmatrix}
K_{1,1} & \cdots & K_{1,N_x} \\
\vdots & \ddots & \vdots \\
K_{N_y,1} & \cdots & K_{N_y,N_x}
\end{bmatrix}
$$

- Output (**Y**) dimension:

$$
\mathbf{Y} \in \mathbb{R}^{B\times C_{out}\times N_y \times N_x}
$$

- $N_x$: Number of element in x direction.
- $N_y$: Number of element in y direction.
- $C_{out}$ : Output channel number (1 for 2D case).
- $B$     : Batch Size.

## Author

Pseudo-Callina 
