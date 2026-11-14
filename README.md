# Velostat Pressure Array Calibration
This repository provides the experimental dataset and Python analysis pipeline supporting the manuscript “Limits of Learning-Based Calibration for Velostat Pressure-Sensing Arrays: A Multi-Session Study Towards Pressure Ulcer Monitoring”.  
The study compares linear and neural network calibration methods for a 4×4 Velostat pressure-sensing array, examining pressure estimation, spatial localisation and sensor artefacts under controlled loading. Chronological validation assesses generalisation to future acquisition sessions.

**Authors:** Padma Michela Ricca, Dr Ben Oldfrey  
**Manuscript title:** Limits of Learning-Based Calibration for Velostat Pressure-Sensing Arrays: A Multi-Session Study Towards Pressure Ulcer Monitoring  

## Repository contents
- `Velostat_Calibration_Pipeline.ipynb` — notebook containing the complete calibration and modelling pipeline.
- `data.zip` — experimental dataset collected separately during the study and subsequently used by the notebook, available from the `Releases` section of this repository.
- `Supporting-Technical-Document.pdf` — supplementary materials accompanying the manuscript.
- `.gitignore` — excludes temporary Python and Jupyter files from version control.

## Dataset
The dataset contains 12 formal acquisition sessions, with 54 acquisition units per session (648 units and 1,315,133 frames in total).  
Data collection uses the recorded sensor channels together with the corresponding nominal pressure and spatial ground-truth labels.  
The original dataset structure is retained so that the integrity checks and session-level analysis implemented in the notebook can be reproduced directly.

## Analysis pipeline
The notebook includes:
- data loading and integrity checks;
- preprocessing of the 16 sensor channels;
- exploratory analysis of the sessions;
- chronological forward validation and model selection;
- comparison of per-taxel linear, Ridge, MLP, LSTM and GRU models;
- final evaluation on test sessions;
- pressure and spatial prediction metrics; 
- additional analyses of sensor behaviour, including creep, hysteresis, drift and crosstalk.

Generated figures and tables are automatically saved during execution to ensure better quality.

## Reproducing the analysis
The analysis was developed and tested in Google Colab.

1. Download `data.zip` from the Releases section of this repository.
2. Open `Velostat_Calibration_Pipeline.ipynb`.
3. Upload `data.zip` to the `/content/` directory.
4. Run the notebook sequentially from top to bottom.

The notebook extracts the dataset to `/content/data/` and saves generated outputs to `/content/final_results/`.

## Software requirements
The pipeline uses Python 3 and the following main packages:

- NumPy
- pandas
- Matplotlib
- scikit-learn
- PyTorch

PyTorch uses a CUDA-enabled GPU when available and falls back to the CPU otherwise.

## Reproducibility and research scope
Random seeds used during model development and final evaluation are defined explicitly in the notebook. Session-level chronological separation is maintained throughout validation and final evaluation to prevent temporal data leakage.

The findings indicate that cross-channel and nonlinear modelling improve calibration accuracy, while recurrent architectures provide no consistent advantage over a memoryless neural network. Remaining prediction errors and spatial crosstalk limit practical performance.

The system has not been clinically validated and is not suitable for clinical pressure monitoring in its present form.

## Use and licensing
The repository is provided to support scientific transparency, independent verification and reproducibility of the accompanying manuscript.
No open-source license has been selected, therefore, standard copyright applies.
