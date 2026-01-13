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

## Benchmark Results

This section presents the official benchmark results on the DFGOVD dataset. These scores serve as baselines for the community to evaluate and compare new methods. The leaderboard is maintained to ensure fair and transparent comparison.

### Official Benchmark Leaderboard

The following table lists the performance of baseline methods evaluated on the DFGOVD **test set**. All models were trained on the official training set and evaluated under the same conditions.

|        Method                   |  Backbone   | AP50 |AP75 |  AP85 | AP50:95 |    Aug   |   Batch Size|                                                 Config                                                     |            
| :--------------------------------------------------------------------------: | :---------------: | :-----: | :-----: | :-----: |:--------: | :-: | :--------: | :------------------------------------------------------------------------------------------------------------: | 
| RetinaNet-O           | R-50-FPN |	53.00 	|	48.41 	|	35.30 	|	40.79 | - |2 |  [rotated_retinanet_obb_r50_fpn_1x_dfgovd_le135](code/mmrotate/configs/dfgovd/rotated_retinanet_obb_r50_fpn_1x_dfgovd_le135.py)  |
| R<sup>3</sup>Det      | R-50-FPN |	64.06 	|	55.76 	|	33.80 	|	46.44 | - |2 |  [r3det_tiny_r50_fpn_1x_dfgovd_oc](code/mmrotate/configs/dfgovd/r3det_tiny_r50_fpn_1x_dfgovd_oc.py)  |
| S<sup>2</sup>A-Net    | R-50-FPN |	65.43 	|	59.13 	|	38.52 	|	48.84 | - |2 |  [s2anet_r50_fpn_1x_dfgovd_le135](code/mmrotate/configs/dfgovd/s2anet_r50_fpn_1x_dfgovd_le135.py)  |
| FCOS-O                | R-50-FPN |	66.26 	|	60.84 	|	45.18 	|	51.66 | - |2 |  [rotated_fcos_r50_fpn_1x_dfgovd_le90](code/mmrotate/configs/dfgovd/rotated_fcos_r50_fpn_1x_dfgovd_le90.py)  |
| DFDet                 | R-50-FPN |	69.59 	|	62.14 	|	44.30   | 52.84 | - |2 |  [dfdet_r50_fpn_1x_dfgovd_le90](code/mmrotate/configs/dfgovd/dfdet_r50_fpn_1x_dfgovd_le90.py)  |
| Faster R-CNN-O        | R-50-FPN |	69.67 	|	59.72 	|	35.77 	|	49.95 | - |2 |  [rotated_faster_rcnn_r50_fpn_1x_dfgovd_le90](code/mmrotate/configs/dfgovd/rotated_faster_rcnn_r50_fpn_1x_dfgovd_le90.py)  | 
| Gliding Vertex        | R-50-FPN |	70.89 	|	60.31 	|	35.97 	|	50.43 | - |2 |  [gliding_vertex_r50_fpn_1x_dfgovd_le90](code/mmrotate/configs/dfgovd/gliding_vertex_r50_fpn_1x_dfgovd_le90.py)  | 
| Oriented R-CNN        | R-50-FPN |	72.63 	|	66.70 	|	48.01 	|	55.89 | - |2 |  [oriented_rcnn_r50_fpn_1x_dfgovd_le90](code/mmrotate/configs/dfgovd/oriented_rcnn_r50_fpn_1x_dfgovd_le90.py)  |
| ReDet                 | ReR-50-ReFPN |	72.87 	|	67.15 	|	48.13 	|	56.19 | - |2 |  [redet_re50_refpn_1x_dfgovd_le90](code/mmrotate/configs/dfgovd/redet_re50_refpn_1x_dfgovd_le90.py)  | 
| RoI Transformer       | R-50-FPN     |	74.59 	|	67.87 	|	47.21 	|	56.87 | - |2 |  [roi_trans_r50_fpn_1x_dfgovd_le90](code/mmrotate/configs/dfgovd/roi_trans_r50_fpn_1x_dfgovd_le90.py)  | 
| D-DETR-O              | R-50-FPN     |	62.13 	|	47.73 	|	26.58 	|	42.19 | - |2 |  [deformable_detr_r50_dfgovd_1x_le90](code/mmrotate/configs/dfgovd/deformable_detr_r50_dfgovd_1x_le90.py)  |
| RQFormer              | R-50-FPN     |	70.88 	|	65.83 	|	50.62 	|	56.29 | - |2 |  [rroiformer_r50_q500_layer2_sq1_dq1_t0.9_1x_dfgovd_le90](code/mmrotate/configs/dfgovd/rroiformer_r50_q500_layer2_sq1_dq1_t0.9_1x_dfgovd_le90.py)  |
| ARS-DETR              | R-50-FPN     |	73.10 	|	69.19 	|	53.95 	|	58.57 | - |2 |  [dn_arw_arm_arcsl_rdetr_r50_dfgovd_1x_le90](code/mmrotate/configs/dfgovd/dn_arw_arm_arcsl_rdetr_r50_dfgovd_1x_le90.py)  |
| OrientedFormer        | R-50-FPN     |	74.62 	|	69.77 	|	53.19 	|	59.17 | - |2 |  [orientedformer_r50_q300_layer2_head64_point32_1x_dfgovd_le90](code/mmrotate/configs/dfgovd/orientedformer_r50_q300_layer2_head64_point32_1x_dfgovd_le90.py)  |
| SFRNet                | R-50-FPN     |	75.35 	|	69.01 	|	49.60 	|	58.11 | - |2 |  [sfr_oriented_rcnn_r50_fpn_1x_dfgovd_le90](code/mmrotate/configs/dfgovd/sfr_oriented_rcnn_r50_fpn_1x_dfgovd_le90.py)  |
| DRNet                 | R-50-FPN     |	76.49 	|	67.36 	|	45.72 	|	56.75 | - |2 |  [drnet_r50_fpn_1x_dfgovd_le90](code/mmrotate/configs/dfgovd/drnet_r50_fpn_1x_dfgovd_le90.py)  |
| PCLDet                | ReR-50-ReFPN |	76.50 	|	70.68 	|	49.68 	|	58.70 | - |2 |  [con_redet_re50_refpn_1x_dfgovd_le90](code/mmrotate/configs/dfgovd/con_redet_re50_refpn_1x_dfgovd_le90.py)  |
| PETDet                | ReR-50-ReFPN |	78.87 	|	72.93 	|	52.51 	|	61.01 | - |2 |  [petdet_r50_fpn_1x_dfgovd_le90](code/mmrotate/configs/dfgovd/petdet_r50_fpn_1x_dfgovd_le90.py)  |

**Evaluation Metric:** We report the standard mean Average Precision (mAP) for oriented object detection, including AP50, AP75, AP85, and AP50:95. For a detailed definition, please refer to the MMRotate documentation.

## License

This codebase is released under the **Apache License 2.0**. This is a permissive license that allows for both academic and commercial use, with requirements for attribution and state changes.

**Key Points of the License:**
*   ✅ **Permits:** Commercial use, modification, distribution, patent use, and private use.
*   ✅ **Requires:** Attribution and inclusion of the original license/copyright notice.
*   ✅ **Provides:** An express grant of patent rights from contributors.
*   ❌ **Does Not:** Hold the original authors liable for damages, or require that modified versions be released under the same license (copyleft).

For the full legal text, please see the [LICENSE_code.md](../LICENSE_code.md) file.

The DFGOVD **dataset** itself is shared under a different license (CC BY-NC-SA 4.0). For details, see the [LICENCE_data.md](../LICENCE_data.md) file.

## Contact
If you have any problems or feedback on our work, please contact: jinqingzheng@tju.edu.cn.

We welcome constructive feedback and contributions to improve this benchmark for the research community.
