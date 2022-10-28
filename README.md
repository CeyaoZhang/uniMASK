# Introduction 

uniMASK is a generalization of BERT models with flexible abstractions for performing inference on subportions of 
sequences. Masking and prediction can occur both on the token level (as in traditional transformer), or even on 
subportions of tokens.

# Getting Started
To install uniMASK, run:

```bash
conda create -n uniMASK python=3.7
conda activate uniMASK
pip install -e .
```

uniMASK requires [D4RL](https://github.com/Farama-Foundation/D4RL).
You may install as detailed [in the D4RL repo](https://github.com/Farama-Foundation/D4RL#setup), e.g., by running:
```bash
pip install git+https://github.com/Farama-Foundation/d4rl@master#egg=d4rl
```

For CUDA support, you may need to reinstall `pytorch` in CUDA mode, for example:
```bash
pip install torch --extra-index-url https://download.pytorch.org/whl/cu116
```

To verify that the installation was successful, run `pytest`.

# Reproducing results from the paper
### Minigrid heatmap (figure 7)
Note: Reproducing all runs can a long time. We recommend parallelizing runs.
In each script, the first line (comment) contains an example of how to use GNU Parallel towards this end.

1. Run the commands found in `minigrid_repro.sh`.
2. Fine-tune the pre-trained models generated in the previous step by running the commands in `minigrid_ft_repro.sh`.
You may want to parallelize these runs as above.
3. Generate the heatmaps from these runs by running `minigrid_heatmap.sh` (no parallelization here).

# File structure
- `data/`: where rollouts (`datasets`) and trained models (`transformer_runs`) are stored. 
- `envs/`: data-handling and evaluation for each supported environment. Currently
- `scripts/`:
- `batches.py`: has all data pipeline processing classes (`FactorSeq, TokenSeq, FullTokenSeq, Batch, SubBatch`)
- `sequences.py`:
- `trainer.py`:
- `transformer.py`: contains the transformer model class itself.
- `transformer_train.py`: interface and config setting for training a transformer, through `Trainer` class.
- `utils.py`: misc utilities, namely math functions, gpu handling, profiling, etc.
- `transformer_eval.py`: interface for getting predictions from transformer (currently empty).