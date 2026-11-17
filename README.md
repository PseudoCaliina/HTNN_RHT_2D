
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

## Author

Pseudo-Callina 
2026/11/17
