# Path Planning Transformer

Transformer-based path planning on 2D grid maps, with notebook experiments and standalone evaluation scripts.

## Quick Start

Use the project virtual environment, then run the evaluator from this directory:

```bash
cd /media/zvi/E69CDDBA9CDD8589/Aregawi
/media/zvi/E69CDDBA9CDD8589/Aregawi/offroad/.venv/bin/python evaluate.py
```

The default evaluation:

- Loads `gpt2-path-20x20-scratch31/`.
- Uses a 20x20 grid with multiple obstacle blocks.
- Plans from `(18, 1)` to `(1, 19)`.
- Allows only adjacent movement, including diagonal neighbors.
- Saves plots to `evaluation_results/`.

Useful options:

```bash

python evaluate.py --mode both
python evaluate.py --start_y 0 --start_x 0 --goal_y 19 --goal_x 19
python evaluate.py --model_dir ./gpt2-path-20x20-scratch31
```


## Main Files

| File | Purpose |
|---|---|
| `evaluate.py` | Loads a trained Transformer, generates paths, verifies movement, and saves visualizations. |
| `utils.py` | Model, tokenizer, path-formatting, and coordinate-extraction utilities. |
| `train.py` | Trains the path-planning Transformer. |
| `prepare_dataset_to_to_model.py` | Prepares pickle path data for model training. |
| `generate_path_dataset.py` | Standalone A* generator for creating synthetic obstacle-grid paths in a pickle file. |
| `gpt2-path-20x20-scratch31/` | Saved model and tokenizer used by the evaluator. |

## Path Notebooks

### `path_generation.ipynb`

A self-contained synthetic-grid experiment. It:

1. Creates a 20x20 grid with rectangular obstacles.
2. Finds shortest paths with eight-directional A*.
3. Generates many start-goal/path records.
4. Saves the records as pickle data.
5. Visualizes sample paths in 2D and on elevation terrain.

The notebook is useful for understanding dataset creation. It does not train the Transformer. For repeatable dataset generation without Jupyter, use:

```bash
python generate_path_dataset.py --num-paths 1000 --output paths_dataset.pkl
```

### `offroad/Scratch.ipynb`

Contains the original grid path-planning experiment from which the standalone Transformer scripts were organized. It is useful for tracing the experimental workflow, while `train.py` and `evaluate.py` provide the command-line workflow.

### `offroad/` terrain notebooks

The `offroad/` directory contains terrain-aware planners and experiments using elevation maps, slope costs, time-optimal objectives, CNN/Transformer models, and benchmark datasets. These are separate from the simple flat obstacle-grid experiment.

## Dataset Record Format

Synthetic path pickle files contain a list of dictionaries:

```python
{
    "start": (row, column),
    "goal": (row, column),
    "path": [(row, column), ...],
    "cost": 12.34,
    "obstacles": [(row, column), ...]
}
```

Coordinates use `(row, column)` order. Plotting code converts them to `(x, y)` when necessary.

## Requirements

Install the main dependencies with:

```bash
pip install -r requirements.txt
```

The synthetic A* generator only requires NumPy. Model training and evaluation additionally require PyTorch, Transformers, Datasets, Tokenizers, and Matplotlib.
