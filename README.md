# Path Planning Transformer

This repository contains the implementation of a Transformer-based
path-planning framework for autonomous navigation on 2D grid maps.

## Repository Contents

- `path_generation.ipynb` — Generates expert shortest-path trajectories used to construct the training dataset.
- `training_and_evaluation.ipynb` — Contains dataset preparation, model definition, training, and evaluation.

## Requirements

The implementation requires Python and the packages imported in the notebooks.

## Usage

The notebooks should be executed in the following order:

### 1. Path Generation

Open `path_generation.ipynb` and execute the cells in order to generate the expert path dataset.

### 2. Training and Evaluation

Open `training_and_evaluation.ipynb` and execute the cells in order to prepare the dataset, train the Transformer model, and perform path-planning evaluation.

## Trained Model

Intermediate training checkpoints and trained model files are not included in this repository due to their size. The training procedure required to reproduce the model is provided in `training_and_evaluation.ipynb`.
