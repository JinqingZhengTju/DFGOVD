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
