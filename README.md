<div align="center"> 

<h1>✨DFGOVD✨</h1> 

[![Typing SVG](https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=18&duration=2000&pause=200&center=true&vCenter=true&multiline=true&random=false&width=500&height=120&lines=DFGOVD+:;A+New+Dataset+and+Benchmark+for;+Drone+Fine-Grained+Oriented+Vehicle+Detection;+in+the+wild)](https://git.io/typing-svg)

</div>

## Introduction
<div align=center>
<img src="docs/DFGOVD-samples.png" width="800"/>
</div>
This is the official implementation of the benchmark of Drone Fine-Grained Oriented Vehicle Detection (DFGOVD). In this paper, we construct DFGOVD, the first large-scale and comprehensive FGOVD dataset for drone-based scenes. The dataset comprises 33,669 images and 816,239 vehicle instances spanning 53 categories and captures subtle distinctions in vehicle appearance, size, and functionality. We benchmark state-of-the-art oriented object detection methods on the DFGOVD dataset, exposing its inherent complexity and challenge.

## Benchmark for DFGOVD

|        Method                   |  Backbone   | AP50 |AP75 |  AP85 | AP50:95 |    Aug   |   Batch Size|                                                 Config                                                     |            
| :--------------------------------------------------------------------------: | :---------------: | :-----: | :-----: | :-----: |:--------: | :-: | :--------: | :------------------------------------------------------------------------------------------------------------: | 
| RetinaNet-O           | R-50-FPN |	53.00 	|	48.41 	|	35.30 	|	40.79 | - |2 |  [rotated_retinanet_obb_r50_fpn_1x_dfgovd_le135]()  |
| R<sup>3</sup>Det      | R-50-FPN |	64.06 	|	55.76 	|	33.80 	|	46.44 | - |2 |  [r3det_tiny_r50_fpn_1x_dfgovd_oc]()  |
| S<sup>2</sup>A-Net    | R-50-FPN |	65.43 	|	59.13 	|	38.52 	|	48.84 | - |2 |  [s2anet_r50_fpn_1x_dfgovd_le135]()  |
| FCOS-O                | R-50-FPN |	66.26 	|	60.84 	|	45.18 	|	51.66 | - |2 |  [rotated_fcos_r50_fpn_1x_dfgovd_le90]()  |
| DFDet                 | R-50-FPN |	69.59 	|	62.14 	|	44.30   | 52.84 | - |2 |  [dfdet_r50_fpn_1x_dfgovd_le90]()  |
| Faster R-CNN-O        | R-50-FPN |	69.67 	|	59.72 	|	35.77 	|	49.95 | - |2 |  [rotated_faster_rcnn_r50_fpn_1x_dfgovd_le90]()  | 
| Gliding Vertex        | R-50-FPN |	70.89 	|	60.31 	|	35.97 	|	50.43 | - |2 |  [gliding_vertex_r50_fpn_1x_dfgovd_le90]()  | 
| Oriented R-CNN        | R-50-FPN |	72.63 	|	66.70 	|	48.01 	|	55.89 | - |2 |  [oriented_rcnn_r50_fpn_1x_dfgovd_le90]()  |
| ReDet                 | ReR-50-ReFPN |	72.87 	|	67.15 	|	48.13 	|	56.19 | - |2 |  [redet_re50_refpn_1x_dfgovd_le90]()  | 
| RoI Transformer       | R-50-FPN     |	74.59 	|	67.87 	|	47.21 	|	56.87 | - |2 |  [roi_trans_r50_fpn_1x_dfgovd_le90]()  | 
| D-DETR-O              | R-50-FPN     |	62.13 	|	47.73 	|	26.58 	|	42.19 | - |2 |  [deformable_detr_r50_dfgovd_1x_le90]()  |
| RQFormer              | R-50-FPN     |	70.88 	|	65.83 	|	50.62 	|	56.29 | - |2 |  [rroiformer_r50_q500_layer2_sq1_dq1_t0.9_1x_dfgovd_le90]()  |
| ARS-DETR              | R-50-FPN     |	73.10 	|	69.19 	|	53.95 	|	58.57 | - |2 |  [dn_arw_arm_arcsl_rdetr_r50_dfgovd_1x_le90]()  |
| OrientedFormer        | R-50-FPN     |	74.62 	|	69.77 	|	53.19 	|	59.17 | - |2 |  [orientedformer_r50_q300_layer2_head64_point32_1x_dfgovd_le90]()  |
| SFRNet                | R-50-FPN     |	75.35 	|	69.01 	|	49.60 	|	58.11 | - |2 |  [sfr_oriented_rcnn_r50_fpn_1x_dfgovd_le90]()  |
| DRNet                 | R-50-FPN     |	76.49 	|	67.36 	|	45.72 	|	56.75 | - |2 |  [drnet_r50_fpn_1x_dfgovd_le90]()  |
| PCLDet                | ReR-50-ReFPN |	76.50 	|	70.68 	|	49.68 	|	58.70 | - |2 |  [con_redet_re50_refpn_1x_dfgovd]()  |
| PETDet                | ReR-50-ReFPN |	78.87 	|	72.93 	|	52.51 	|	61.01 | - |2 |  [petdet_r50_fpn_1x_dfgovd_le90]()  |

## Code

## Data 


## License

This repository and its associated Data Paper introduce the **DFGOVD** dataset. Different components are governed by **different licenses and access terms**. Please review the following carefully.

> **⚠️ Important**: For the complete and authoritative licensing information, please see the root **[LICENSE.md](./LICENSE.md)** file.

### 1. Source Code (`/code` Directory)
The source code contained within the [`/code`](./code) directory is licensed under the **Apache License, Version 2.0**.

**Key Permissions in Plain Language:**
*   **You are free to**: use, copy, modify, and distribute this code, including for commercial purposes.
*   **You must**: retain the original copyright notice and the full text of the license in any distributions.
*   **Disclaimer**: The code is provided "AS IS", without warranty of any kind.

For the complete legal terms, see: [**LICENSE_code.txt**](./LICENSE_code.txt).

### 2. The DFGOVD Dataset: Documentation, Samples & Full Data

#### a) Dataset Documentation & Metadata (`/data` Directory)
The documentation, descriptions, and metadata within the [`/data`](./data) directory that describe the `DFGOVD` dataset are licensed under the **Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License (CC BY-NC-SA 4.0)**.

**Key Terms in Plain Language:**
*   **You are free to**: share and adapt this material under these terms:
    1.  **Attribution (BY)**: You must give appropriate credit.
    2.  **NonCommercial (NC)**: **You may not use this material for commercial purposes.**
    3.  **ShareAlike (SA)**: Derivatives must be shared under the **same license**.
*   **Core Restriction**: This license **explicitly prohibits any commercial use**.

For the complete legal text, see: [**LICENSE_data.txt**](./LICENSE_data.txt).

#### b) Sample Data
The **sample data files** included in the `/data` directory are for demonstration and testing. Their use is **also governed by the CC BY-NC-SA 4.0 license** stated above.

#### c) Complete DFGOVD Dataset (Available Upon Request)
The **full `DFGOVD` dataset** is not publicly distributed in this repository.

**Access Terms:**
1.  **License**: Access is subject to a **custom Data Use Agreement (DUA)**, with terms at least as restrictive as CC BY-NC-SA 4.0 (non-commercial, requires attribution).
2.  **How to Access**: Researchers must contact the authors (e.g., by opening a GitHub Issue) to request access and agree to the DUA.
3.  **Mandatory Citation**: Use of the dataset **must** cite our associated Data Paper.

### ⚠️ Important Notices
*   **License Separation**: The licenses for the code and the dataset materials are separate. Using both requires compliance with both sets of terms.
*   **Commercial Use**:
    *   The **source code (Apache 2.0)** allows commercial use.
    *   **All dataset materials (CC BY-NC-SA 4.0) PROHIBIT commercial use** without explicit permission.
*   **Definitive Source**: This summary is for convenience. The root **[LICENSE.md](./LICENSE.md)** file is the definitive document for all licensing matters.
