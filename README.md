# Searching for HWW Anomalous Couplings with Simulation-Based Inference

This repository contains the code for my [Master’s Thesis](https://repository.cern/records/edyrv-bwg35), later extended into a peer-reviewed [publication](https://journals.aps.org/prd/abstract/10.1103/29xq-b66r) in Physical Review D. 

The analysis benchmarks the simulation-based inference techniques **ALICES** (Approximate Likelihood with Improved Cross-Entropy Estimator and Score) and **SALLY** (Score Approximates Likelihood LocallY) against the traditional approachesof using histograms of kinematic and angular observables.

This work uses **MadMiner** version `0.9.3` ([GitHub](https://github.com/madminer-tool/madminer)) and requires **MadGraph** version `>= 3.3.1` if generating samples.

## Setup

Before generating samples (either locally or in a batch system), set up the SMEFTsim model and restrict card by running:

```bash
source 0_setup_SMEFTsim_model.sh
```

## Workflow

To run the analysis, execute the scripts in the following order:

- **`1_setup.py`**: Defines the Wilson coefficient and morphing setup and creates a setup file.

- **`2a_gen_signal.py`**: Generates signal samples or prepares files for batch system execution.

- **`2b_gen_background.py`**: Generates background samples or prepares files for batch system execution.

- **`2c_reweight_signal.py`**: This step is optional, but if running generation on multi-core mode, it is recommended to do the reweighting separately.

- **`3a_run_delphes_analysis.py`**: Defines detector-level observables and performs Delphes-based analysis.

- **`3b_run_delphes_analysis_SLURM.py`**: Use this script instead of **`3a_run_delphes_analysis.py`** if running on SLURM. This uses both **`3a_run_delphes_analysis.py`** and **`3c_run_delphes_analysis_SLURM.sh`** scripts.

- **`4_analysis_sample_combiner.py`**: Combines analyzed samples.

- **`5a_alices_training.py`**: Performs data augmentation and training for ALICES.

- **`5b_sally_training.py`**: Performs data augmentation and training for SALLY.

- **`6_evaluate_limits.py`**: Computes limits using the full likelihood ratio (asymptotic limit) for ALICES and SALLY.

## Usage

Each script provides an argument parser. Run:

```bash
python script_name.py -h
```

to see available options.

Each scenario (**parton_level_validation**, **1D_CP_odd**, **1D_CP_even**, **2D_low_pT**, **2D_high_pT**) has a corresponding folder with a similar workflow and a specific **config file** that defines its parameters and settings.

## Reference

This work builds on the paper:  
[*Simulation-based inference in the search for CP violation in leptonic WH production*](https://arxiv.org/abs/2308.02882).  
The code for that study ([GitHub](https://github.com/rbarrue/sally_cpv_wh)) was used as a starting basis.
