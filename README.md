# IRES — Battery State of Health and Remaining Useful Life

Instrumentation for Renewable Energy project with Python and MATLAB pipelines, Arduino battery-monitor firmware, saved model artifacts, and recorded evaluation outputs.

## What the project does

State of Health (SOH) describes a battery's remaining usable capacity relative to its nominal capacity. Remaining Useful Life (RUL) estimates the cycles left until an end-of-life threshold. This project uses an 80% SOH threshold in its documented lifecycle workflow.

The Python workflow prepares lifecycle data, extracts cycle-level features, compares regression models, saves model artifacts, and supports an Arduino serial measurement/dashboard path. Traditional model artifacts and recurrent neural-network artifacts are included. The MATLAB workflow compares ANN, SVR, and Random Forest base learners and uses out-of-fold predictions for a stacked meta-learner. Battery-grouped splits are described in the MATLAB documentation to keep one battery's cycles from crossing evaluation partitions.

The Arduino firmware supplies an instrumentation path; dataset training, live sensor measurement, and the standalone empirical GUI are distinct parts of the project. The GUI simulates degradation using temperature and C-rate assumptions. Recorded results are included as project outputs, without claiming that every saved model or reported metric has been independently reproduced.

## Project documents

- [Project report](IRES-project-report.pdf)
- [Presentation](IRES-presentation.pdf)

## Download

Extract **IRES-source-and-results.zip**. Extract every **IRES-models-XX.zip** archive into the same directory; each contains complete files, and together they populate `python/models/`.

- `python/`: dataset preparation, feature extraction, model training, serial acquisition, dashboard, evaluation scripts, and recorded results.
- `matlab/`: ANN, Random Forest, SVR, and stacking pipeline with its original README.
- `arduino/`: additional local firmware (`unodata.ino`).
- `standalone/`: empirical battery degradation GUI; this is a simulation, not a trained prediction pipeline.
- `results/` and `legacy-project-data/`: local plots, presentation, model outputs, and earlier model artifacts.

## Python setup

From the extracted `python` directory:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python main.py
```

The existing dependency file is unpinned. Some optional neural-network paths may require additional dependencies; this upload does not establish a fully reproduced training environment. Inspect `config.py` and configure `NASA_DATA_PATH` and `NH_ECYCLE_PATH` for your own dataset locations. The original README inside the archive explains the intended preparation/training/dashboard workflow and the 80% SOH end-of-life convention. Arduino serial port selection is machine-specific.

## MATLAB

Read `matlab/README.md`. The local pipeline documents MATLAB R2024a/R2024b with Statistics and Machine Learning Toolbox and Deep Learning Toolbox. Configure the dataset path before running `main_SOH_Prediction.m`.

## Data and validation status

Third-party raw datasets, downloaded reference papers, personal coursework PDFs, local logs, virtual environments, and caches are excluded. Obtain the NASA battery lifecycle dataset and any other data from their original providers under the applicable terms. Processed cycle data and recorded result files from the project archive are retained; their presence does not independently validate accuracy claims. The model files were copied without deserializing or executing them. This upload includes syntax and archive-integrity checks, not a reproduced model-training or hardware test.

No open-source license has been adopted. Do not connect batteries directly to Arduino analog pins; follow the original firmware documentation and use correctly rated measurement interfaces.
