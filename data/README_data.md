# DFGOVD Dataset

## Overview
The DFGOVD (Drone Fine-Grained Oriented Vehicle Detection) dataset is the first large-scale and comprehensive FGOVD dataset for drone-based scenes. The dataset comprises 33,669 images and 816,239 vehicle instances spanning 53 categories and captures subtle distinctions in vehicle appearance, size, and functionality. 

- **Total Images:** 33,669
- **Total Annotated Instances:** 816,239
- **Categories:** 53 fine-grained vehicle categories
- **Annotation Format:** Oriented Bounding Boxes (OBB)
- **Primary Task:** Fine-Graided Oriented Vehicle Detection (FGOVD)

## Directory Structure
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
## Data Splits
The DFGOVD dataset is officially partitioned into training, validation, and test sets to facilitate standardized benchmarking, model development, and fair evaluation. The detailed statistics for each split are as follows: 
| Split | Number of Images | Number of Instances | Primary Purpose |
| :--- | :---: | :---: | :--- |
| **Training Set**   | 20,201 | 491,188 | Model training and parameter learning. |
| **Validation Set** | 3,367 | 80,720 | Hyperparameter tuning and model validation during training. |
| **Test Set**       | 10,101 | 244,331 | **Final evaluation** and reporting of benchmark results. |
| **Total**          | **33,669** | **816,239** | The complete DFGOVD dataset. |

**Usage Note:** To ensure fair comparison and reproducibility, we require that researchers report performance metrics **only on the official test set**. The validation set should be used for model selection and ablation studies. Please do not train models on the combined training and validation sets for final test evaluation.

## Annotation Format
The annotations for each image are provided in separate text files within the `labelTxt/` directories, following a widely-used format for oriented object detection. Each annotation file shares the same name as its corresponding image (e.g., V000001.txt for V000001.jpg) and contains lines defining each object instance. Each line in an annotation file represents one object instance and consists of 10 fields, formatted as follows:
```
x1 y1 x2 y2 x3 y3 x4 y4 category difficulty
```
## Usage Instructions
### 1. Using the Full Dataset
After obtaining access to the complete dataset:

- **Preprocessing:** Use the provided scripts in [/code/tools/dfgovd](./code/tools/dfgovd) for data conversion

### 2. Integration with MMRotate
The dataset is designed to work seamlessly with the MMRotate framework. Example configuration:
```
dataset_type = 'DFGOVDDataset'
data_root = 'data/split_ss_DFGOVD/'
```

## Data Access and Licensing
*   **Sample Data:** We have released sample data located in the [`/data/sample_data`](./data/sample_data) directory to demonstrate the format and structure of our dataset. This sample data licensed under **[CC BY-NC-SA 4.0](./LICENSE_data.txt)**.
*   **Complete DFGOVD Dataset:** The complete DFGOVD dataset is not yet publicly released. It is planned for future release under **[CC BY-NC-SA 4.0](./LICENSE_data.txt)** and is currently available only upon request. To apply for access (non-commercial only), please contact: jinqingzheng@tju.edu.cn.

## Ethical Considerations and Disclaimer

The DFGOVD dataset was collected from real-world scenarios. Researchers and users of this dataset should be aware of and comply with the following:

1.  **Privacy:** The dataset may contain information that could be considered sensitive. All data has been processed to remove **personally identifiable information (PII)** to the best of our ability. However, we **cannot guarantee** that all privacy-relevant information has been entirely eliminated.
2.  **Intended Use:** This dataset is provided **strictly for non-commercial academic research purposes** in fields such as computer vision and remote sensing. Any use of the dataset for surveillance, identification, or any other purposes that may infringe upon individual privacy or rights is **strictly prohibited**.
3.  **Disclaimer of Liability:** The authors and affiliated institutions **shall not be held liable** for any claims, damages, or other liabilities arising from the use or misuse of this dataset, including but not limited to any privacy violations.
4.  **User Responsibility:** By using this dataset, you agree to assume full responsibility for your use of the data and to comply with all applicable local, national, and international laws and regulations regarding data privacy and protection.


## Contact
For any questions regarding the dataset, please contact: jinqingzheng@tju.edu.cn.

