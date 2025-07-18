<div align="center">
    <h1>Between Can and Will: Embodied Trajectory Prediction through Affordance and Intention</h2>
    <strong>AAAI 2026</strong>
    <br>
        Anonymous authors
    <p>
        <h45>
                Anonymous affiliation
            <br>
        </h5>
    </p>
</div>

## 📝 To-do list

- [x] Release anonymous project
- [ ] Release anonymous codes
- [ ] Make project paper publicly available
- [ ] Release project and codes
- [ ] Release model checkpoints

## 🚗 Abstract
We introduce the Selective Embodied Learning for Trajectory Prediction Framework (SELF), a trajectory prediction framework grounded in embodied intelligence. SELF redefines prediction as a dynamic perception--action loop rather than static inference, modeling how agents perceive and act upon affordances in complex traffic environments. It comprises a Selective Interaction Encoder (SIE) that selectively captures immediate, behaviorally-relevant interactions, a Affordance Aggregation Module (AAM) that models scenario-level constraints through saliency-based relational encoding, and a Intention Reasoning Module (IRM) that adaptively integrates these cues via gated attention. Together, these modules instantiate a closed-loop perception system capable of dynamically recalibrating predictions in response to evolving affordances. The model outputs multi-modal trajectory distributions through a confidence-weighted prediction head, optimized via a composite loss that balances accuracy, diversity, and temporal consistency. Extensive evaluations across Argoverse 2, NGSIM, MoCAD, and HighD show that SELF consistently achieves state-of-the-art performance with interpretable, behaviorally plausible predictions, demonstrating its potential for robust and context-aware motion predicting in real-world autonomous driving scenarios.

## 🎞️ Pipeline
```
coming soon
```

## 🛠️ Configure programming environment

### Set up a new virtual environment and install dependency packpages
```bash
conda create -n self python=3.10
conda activate self
pip install torch==2.0.1 torchvision==0.15.2 torchaudio==2.0.2 --index-url https://download.pytorch.org/whl/cu118
pip install -r requirements.txt
pip install natten==0.17.3+torch200cu118 -f https://shi-labs.com/natten/wheels
git clone https://github.com/argoverse/argoverse-api.git
cd argoverse-api
pip install -e .
```

## 🕹️ Prepare the dataset
### Setup [Argoverse 2 Motion Forecasting Dataset](https://www.argoverse.org/av2.html)
```
data
    ├── train
    │   ├── 0000b0f9-99f9-4a1f-a231-5be9e4c523f7
    │   ├── 0000b6ab-e100-4f6b-aee8-b520b57c0530
    │   ├── ...
    ├── val
    │   ├── 00010486-9a07-48ae-b493-cf4545855937
    │   ├── 00062a32-8d6d-4449-9948-6fedac67bfcd
    │   ├── ...
    ├── test
    │   ├── 0000b329-f890-4c2b-93f2-7e2413d4ca5b
    │   ├── 0008c251-e9b0-4708-b762-b15cb6effc27
    │   ├── ...
```

You can follow official [instruction](https://argoverse.github.io/user-guide/getting_started.html#downloading-the-data) to download dataset:

```bash
conda install s5cmd -c conda-forge
```

```bash
#!/usr/bin/env bash

# Dataset URIs
# s3://argoverse/datasets/av2/sensor/ 
# s3://argoverse/datasets/av2/lidar/
# s3://argoverse/datasets/av2/motion-forecasting/
# s3://argoverse/datasets/av2/tbv/

export DATASET_NAME="sensor"  # sensor, lidar, motion_forecasting or tbv.
export TARGET_DIR="$HOME/data/datasets"  # Target directory on your machine.

s5cmd --no-sign-request cp "s3://argoverse/datasets/av2/$DATASET_NAME/*" $TARGET_DIR
```

### Preprocess
```
python preprocess.py -d /path/to/data -p
```

### The structure of the dataset after processing
```
└── data
    └── self_processed
        ├── train
        ├── val
        └── test
```

## 🔥 Train
```bash
# Train
python train.py
```

## ⭐ Val
```bash
# Val
python eval.py checkpoint=/path/to/ckpt
# Test for submission
python eval.py checkpoint=/path/to/ckpt submit=true
```

## 😊 License
Please see [MIT License](https://mit-license.org/).
