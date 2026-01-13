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
- If you encounter any compilation errors when installing MMCV, please ensure that your GCC version meets the requirement and that the CUDA path is correctly set.
- For any version mismatch errors, please double-check that you have installed the correct versions as specified above.






