# DFGOVD Benchmark Code

## Overview

This repository contains the training and evaluation code for benchmarking baseline methods on the DFGOVD dataset, ensuring fair and reproducible results. The implementation is built upon the following open-source frameworks:

- [**MMRotate**](https://github.com/open-mmlab/mmrotate/tree/main) (v0.3.4)
- [**MMDetection**](https://github.com/open-mmlab/mmdetection/tree/2.x) (v2.28.2)
- [**MMCV**](https://github.com/open-mmlab/mmcv/tree/1.x) (v1.7.2)

The code is located in the [`/code`](../code) directory and is licensed under the [**Apache License 2.0**](../LICENSE_code.txt).

## Installation

### Prerequisites
Before installing the codebase, ensure your system meets the following requirements:

- **Operating System:** Linux (recommended) or macOS. Windows is not officially supported but may work via WSL.
- **Python:** 3.7 or higher (3.8 is recommended).
- **PyTorch:** 1.6 or higher.
- **CUDA:** Required for GPU acceleration. We recommend CUDA 10.2 or higher, compatible with your PyTorch version.
- **NCCL:** Required for multi-GPU training (Linux only).
- **GCC:** 5.4 or higher for compiling some dependencies (Linux only).

### Step-by-Step Installation Guide

We recommend using a Python virtual environment (e.g., Conda) to manage dependencies.

**1. Clone this repository and navigate to the code directory:**
```bash
git clone https://github.com/JinqingZhengTju/DFGOVD.git
cd DFGOVD/code
```

**2. Create and activate a Conda environment:**
```bash
conda create -n dfgovd python=3.8 -y
conda activate dfgovd
```

**3. Install PyTorch and torchvision:**
Please refer to the [official PyTorch website](https://pytorch.org/get-started/previous-versions/) for the command that matches your CUDA version.
```bash
# Example for CUDA 11.3
conda install pytorch==1.10.0 torchvision==0.11.0 cudatoolkit=11.3 -c pytorch
```

**4. Install MMCV from source:**
We use the included MMCV (v1.7.2) source code.
```bash
# Navigate to the mmcv directory and install
cd mmcv  # This is inside the /code directory
pip install -r requirements/optional.txt
MMCV_WITH_OPS=1 pip install -e .  # This will compile with CUDA ops
cd ..
```

**5. Install MMDetection from source:**
We use the included MMDetection (v2.28.2) source code.
```bash
# Navigate to the mmdetection directory and install
cd mmdetection
pip install -e .
cd ..
```

**6. Install MMRotate from source:**
We use the included MMRotate (v0.3.4) source code.
```bash
# Navigate to the mmrotate directory and install
cd mmrotate
pip install -e .
cd ..
```

### Verification
You can verify the installation by running a simple Python check:
```bash
python -c "import mmrotate, mmdet, mmcv; print('All imports successful.')"
```

**Troubleshooting Tip:** 
- If you encounter any compilation errors when installing MMCV, please ensure that your GCC version meets the requirements and that the CUDA path is correctly set.
- For any version mismatch errors, please double-check that you have installed the correct versions as specified above.

## Data Preparation

The DFGOVD dataset must be properly organized for the training and evaluation scripts to function correctly.

### 1. Directory Structure
Please organize your dataset according to the structure defined in the main dataset documentation. **For comprehensive details on data organization, annotation format, and splits, please refer to the dedicated [README_data.md](../data/README_data.md) file.**

In brief, the expected structure within the project root is:
```
data/DFGOVD/
├── train/
│   ├── images/
│   └── labelTxt/
├── val/
│   ├── images/
│   └── labelTxt/
└── test/
    ├── images/
    └── labelTxt/
```
A sample dataset is provided in `../data/sample_data` for format verification.

### 2. Quick Setup Script
Use the provided scripts in [/code/mmrotate/tools/data/dfgovd](../code/mmrotate/tools/data/dfgovd) for data conversion after placing your data in the correct location.

### 3. Configuration
The dataset paths are pre-configured in the base configuration file [`/code/mmrotate/configs/_base_/datasets/dfgovd.py`](../code/mmrotate/configs/_base_/datasets/dfgovd.py).

**If your dataset is located elsewhere**, update the `data_root` variable in the relevant model configuration file before training:
```python
# Modify this line to your dataset path
data_root = '/your/custom/path/to/split_ss_DFGOVD/'
```

## Usage

This section provides instructions for training and evaluating with the provided baseline models on the DFGOVD dataset.

### 1. Training a Model

We provide configuration files for some state-of-the-art baseline models in the [`configs/dfgovd`](../code/mmrotate/configs/dfgovd) directory. To train a model, use the `tools/train.py` script.

#### Single GPU Training
```bash
python tools/train.py ${CONFIG_FILE} [optional arguments]
```

**Example:** Train Rotated Faster R-CNN on a single GPU:
```bash
python tools/train.py configs/dfgovd/rotated_faster_rcnn_r50_fpn_1x_dfgovd_le90.py
```

#### Multi-GPU Training
We support distributed training with multiple GPUs using `torch.distributed.launch`.
```bash
bash tools/dist_train.sh ${CONFIG_FILE} ${GPU_NUM} [optional arguments]
```

**Example:** Train Rotated Faster R-CNN on 8 GPUs:
```bash
bash tools/dist_train.sh configs/dfgovd/rotated_faster_rcnn_r50_fpn_1x_dfgovd_le90.py 8
```

**Optional Arguments:**
- `--work-dir ${WORK_DIR}`: Override the working directory (where logs and checkpoints are saved).
- `--resume-from ${CHECKPOINT_FILE}`: Resume training from a checkpoint.
- `--no-validate`: Do not evaluate the checkpoint during training (not recommended).

### 2. Evaluating a Model

To evaluate a trained model on the validation or test set, use the `tools/test.py` script.

#### Single GPU Evaluation
```bash
python tools/test.py ${CONFIG_FILE} ${CHECKPOINT_FILE} [--eval ${EVAL_METRICS}] [--out ${RESULT_FILE}]
```

**Example:** Evaluate a Rotated Faster R-CNN checkpoint and compute mAP:
```bash
python tools/test.py configs/dfgovd/rotated_faster_rcnn_r50_fpn_1x_dfgovd_le90.py work_dirs/rotated_faster_rcnn_r50_fpn_1x_dfgovd_le90/epoch_12.pth --eval mAP
```

#### Multi-GPU Evaluation
```bash
bash tools/dist_test.sh ${CONFIG_FILE} ${CHECKPOINT_FILE} ${GPU_NUM} [--eval ${EVAL_METRICS}] [--out ${RESULT_FILE}]
```

**Example:** Evaluate using 8 GPUs:
```bash
bash tools/dist_test.sh configs/dfgovd/rotated_faster_rcnn_r50_fpn_1x_dfgovd_le90.py work_dirs/rotated_faster_rcnn_r50_fpn_1x_dfgovd_le90/epoch_12.pth 8 --eval mAP
```

**Important:** For fair comparison, please evaluate on the **test set** only once and report the final result. The validation set should be used for development and model selection.


### 3. Using Custom Configuration

You can modify the provided configuration files or create new ones to experiment with different settings. The configuration system is based on MMDetection and MMRotate. Please refer to their documentation for details.

To use a custom configuration file, simply pass its path to the training or evaluation scripts.

### 4. Notes on Reproducibility

- We have fixed random seeds in the provided configuration files to ensure reproducibility. However, note that complete reproducibility may be affected by factors such as the CUDA version, GPU type, and environment.
- The performance reported in the Model Zoo (see next section) is obtained with the default configuration and specific hardware. Slight variations are expected.










