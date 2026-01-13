<div align="center"> 

<h1>✨DFGOVD✨</h1> 

[![Typing SVG](https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=18&duration=2000&pause=200&center=true&vCenter=true&multiline=true&random=false&width=500&height=120&lines=DFGOVD+:;A+New+Dataset+and+Benchmark+for;+Drone+Fine-Grained+Oriented+Vehicle+Detection;+in+the+wild)](https://git.io/typing-svg)

</div>

## Introduction
<div align=center>
<img src="docs/DFGOVD-samples.png" width="800"/>
</div>
This is the official implementation of the benchmark of Drone Fine-Grained Oriented Vehicle Detection (DFGOVD). In this paper, we construct DFGOVD, the first large-scale and comprehensive FGOVD dataset for drone-based scenes. The dataset comprises 33,669 images and 816,239 vehicle instances spanning 53 categories and captures subtle distinctions in vehicle appearance, size, and functionality. We benchmark state-of-the-art oriented object detection methods on the DFGOVD dataset, exposing its inherent complexity and challenge.

## News 🎉
**January 2026:** Our paper **"DFGOVD: A New Dataset and Benchmark for Drone Fine-Grained Oriented Vehicle Detection in the Wild"** has been **accepted for publication by IEEE Transactions on Geoscience and Remote Sensing (TGRS)**!  

## Benchmark for DFGOVD

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

## Code
This repository provides the training and evaluation code for benchmarking baseline methods on the DFGOVD dataset to ensure fair and reproducible results. The implementation is built upon the following open-source frameworks:  [MMRotate](https://github.com/open-mmlab/mmrotate/tree/main) (v0.3.4), [MMDetection](https://github.com/open-mmlab/mmdetection/tree/2.x) (v2.28.2), and [MMCV](https://github.com/open-mmlab/mmcv/tree/1.x) (v1.7.2). The source code is located in the [`/code`](./code) directory. For installation and usage instructions, please refer to [README_code.md](./code/README_code.md). 
## Data 
The DFGOVD dataset comprises 33,669 images, annotated with 816,239 vehicle instances using oriented bounding boxes covering 53 categories. For details on dataset annotation, splits, and usage instructions, please refer to [README_data.md](./data/README_data.md). 
### Data Access
*   **Sample Data:** We have released sample data located in the [`/data/sample_data`](./data/sample_data) directory to demonstrate the format and structure of our dataset. 
*   **Complete DFGOVD Dataset:** The complete DFGOVD dataset is not yet publicly released. It is planned for future release under **[CC BY-NC-SA 4.0](./LICENSE_data.txt)** and is currently available only upon request. To apply for access (non-commercial only), please contact: jinqingzheng@tju.edu.cn.
    
## License
This project uses **multiple licenses** for different components (code, sample data, full dataset). The terms are nuanced. **This section is a summary only.** For the complete and authoritative terms, see the **[LICENSE.md](./LICENSE.md)** file.

### Quick Summary
*   **Source Code (`/code` directory):** Licensed under **[Apache License 2.0](./LICENSE_code.txt)** (allows commercial use).
*   **Sample Data (`/data` directory):** Licensed under **[CC BY-NC-SA 4.0](./LICENSE_data.txt)** (non-commercial only).
*   **Complete DFGOVD Dataset:** **Not yet included** in this repo. Planned for future release under CC BY-NC-SA 4.0. Currently available by request.

### ⚠️ Important Notes
1.  The licenses for code and data are **separate and independent**.
2.  For inquiries or to request the complete dataset, please contact: jinqingzheng@tju.edu.cn.

## Ethical Considerations and Disclaimer

The DFGOVD dataset was collected from real-world scenarios. Researchers and users of this dataset should be aware of and comply with the following:

1.  **Privacy:** The dataset may contain information that could be considered sensitive. All data has been processed to remove **personally identifiable information (PII)** to the best of our ability. However, we **cannot guarantee** that all privacy-relevant information has been entirely eliminated.
2.  **Intended Use:** This dataset is provided **strictly for non-commercial academic research purposes** in fields such as computer vision and remote sensing. Any use of the dataset for surveillance, identification, or any other purposes that may infringe upon individual privacy or rights is **strictly prohibited**.
3.  **Disclaimer of Liability:** The authors and affiliated institutions **shall not be held liable** for any claims, damages, or other liabilities arising from the use or misuse of this dataset, including but not limited to any privacy violations.
4.  **User Responsibility:** By using this dataset, you agree to assume full responsibility for your use of the data and to comply with all applicable local, national, and international laws and regulations regarding data privacy and protection.

## Contact
If you have any problems or feedback on our work, please contact: jinqingzheng@tju.edu.cn.
