# DFGOVD Dataset

## Overview
The DFGOVD (Drone Fine-Grained Oriented Vehicle Detection) dataset is the first large-scale and comprehensive FGOVD dataset for drone-based scenes. The dataset comprises 33,669 images and 816,239 vehicle instances spanning 53 categories and captures subtle distinctions in vehicle appearance, size, and functionality. 

- **Total Images:** 33,669
- **Total Annotated Instances:** 816,239
- **Categories:** 53 fine-grained vehicle categories
- **Annotation Format:** Oriented Bounding Boxes (OBB)
- **Primary Task:** Fine-Graided Oriented Vehicle Detection (FGOVD)

# Directory Structure
The dataset follows the structure below. Upon request, you will receive the data organized as follows:
```bash
data/
├── sample_data/          # Publicly available sample subset for preview
│   ├── images/           # Sample images
│   └── labelTxt/         # Corresponding annotations
├── train/                # Training set (available upon request)
│   ├── images/           # Training images
│   └── labelTxt/         # Training annotations
├── val/                  # Validation set (available upon request)
│   ├── images/
│   └── labelTxt/
└── test/                 # Test set (available upon request)
    ├── images/
    └── labelTxt/
```
# Data Splits
The DFGOVD dataset is officially partitioned into training, validation, and test sets to facilitate standardized benchmarking, model development, and fair evaluation. The detailed statistics for each split are as follows: 
| Split | Number of Images | Number of Instances | Primary Purpose |
| :--- | :---: | :---: | :--- |
| **Training Set**   | 20,201 | 491,188 | Model training and parameter learning. |
| **Validation Set** | 3,367 | 80,720 | Hyperparameter tuning and model validation during training. |
| **Test Set**       | 10,101 | 244,331 | **Final evaluation** and reporting of benchmark results. |
| **Total**          | **33,669** | **816,239** | The complete DFGOVD dataset. |

**Usage Note:** To ensure fair comparison and reproducibility, we require that researchers report performance metrics **only on the official test set**. The validation set should be used for model selection and ablation studies. Please do not train models on the combined training and validation sets for final test evaluation.




