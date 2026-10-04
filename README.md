# EEG Seizure Prediction with LSTM

A CHB-MIT notebook experiment that constructs temporal EEG sequences and trains an LSTM to classify preictal versus non-preictal windows.

## Results

Saved notebook output reports a held-out accuracy of **55%** on 3,196 sequences. For the positive/preictal class, reported precision is **0.84** but recall is only **0.13** (208 of 1,604 positive examples detected). Training logs approaching 99% accuracy do not reflect held-out performance. Outputs were not reproduced locally.

## Architecture

```mermaid
flowchart LR
  D[CHB-MIT EDF recordings] --> P[Resample and epoch EEG]
  P --> L[Label preictal windows]
  L --> Q[Build temporal sequences]
  Q --> M[LSTM classifier]
  M --> E[Held-out sequence report]
```

## Quickstart and verification

The notebook's setup is not reproducible from `requirements.txt`: the notebook uses TensorFlow/Keras but the manifest does not install TensorFlow. Data is also external and no standalone command is provided. The saved notebook outputs were inspected but not rerun here.

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
pip install tensorflow
```

Then open `lstm_model_pipeline.ipynb`, obtain the referenced CHB-MIT files, and update the notebook's data paths. This is a documented setup attempt, not a verified end-to-end quickstart.

## Limitations

- Low preictal recall means most positive windows are missed at the reported threshold.
- Segment accuracy does not describe patient-level warning utility or false alarms per hour.
- Notebook has historical output, hard-coded/data-specific assumptions, and missing TensorFlow dependency.
- Single-patient CHB-MIT exploration is not generalizable evidence.

## Next steps

1. Move preprocessing, training, and evaluation into parameterized Python modules.
2. Pin TensorFlow and all notebook dependencies; add a reproducible environment check.
3. Use patient/time-aware splits and event-level evaluation.
4. Compare alarm thresholds on validation data and report sensitivity with false alarms/hour.
