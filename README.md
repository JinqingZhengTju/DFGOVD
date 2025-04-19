<div align="center"> 

<h1>✨DFGOVD✨</h1> 

[![Typing SVG](https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=18&duration=2000&pause=200&center=true&vCenter=true&multiline=true&random=false&width=500&height=120&lines=DFGOVD+:;A+New+Dataset+and+Benchmark+for;+Drone+Fine-Grained+Oriented+Vehicle+Detection;+in+the+wild)](https://git.io/typing-svg)

</div>

## Introduction
<div align=center>
<img src="imgs/DFGOVD-samples.png" width="800"/>
</div>
This is the official implementation of the benchmark of Drone Fine-Grained Oriented Vehicle Detection. In this paper, we construct a large-scale dataset of Drone Fine-Grained Oriented Vehicle Detection (DFGOVD), which contains 33,669 images collected in multiple complex scenarios and 816,239 instances annotated with 5 categories and 53 subcategories by oriented bounding boxes. To our knowledge, the proposed DFGOVD dataset is the first fine-grained drone vehicle detection dataset, which is valuable for supporting research on more practical drone vehicle detection algorithms. We give the results and models of 12 OOD methods on the DFGOVD. Based on this dataset, we expect more researchers to join the study of fine-grained oriented vehicle detection methods.

## Object samples of each category in the DFGOVD dataset
<div align=center>
<img src="imgs/DFGOVD-class.png" width="800"/>
</div>

## Results and models
DFGOVD

|        Method                   |  Backbone   | AP50 |AP75 |  AP50:95 |    Aug   |   Batch Size|                                                 Config                                                     |                                                                                                                                                                              Model                                                                                                                                                                              |         log|
| :---------------------------------------: | :---------------: | :-----: | :-----: |:--------: | :-: | :--------: | :------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| RetinaNet-O           | R-50-FPN | 53.00   | 48.41 | 40.79 | - |2 |  [rotated_retinanet_obb_r50_fpn_1x_dfgovd_le135]()  |[model]()|[log]()| 
| R<sup>3</sup>Det      | R-50-FPN | 64.06   | 55.76 | 46.44 | - |2 |  [r3det_tiny_r50_fpn_1x_dfgovd_oc]()  |[model]()|[log]()| 
| S<sup>2</sup>A-Net    | R-50-FPN | 65.43   | 59.13 | 48.84 | - |2 |  [s2anet_r50_fpn_1x_dfgovd_le135]()  |[model]()|[log]()| 
| FCOS-O                | R-50-FPN | 66.26   | 60.84 | 51.66 | - |2 |  [rotated_fcos_r50_fpn_1x_dfgovd_le90]()  |[model]()|[log]()| 
| Faster R-CNN-O        | R-50-FPN | 69.67   | 59.72 | 49.95 | - |2 |  [rotated_faster_rcnn_r50_fpn_1x_dfgovd_le90]()  |[model]()|[log]()| 
| Gliding Vertex        | R-50-FPN | 70.89   | 60.31 | 50.43 | - |2 |  [gliding_vertex_r50_fpn_1x_dfgovd_le90]()  |[model]()|[log]()| 
| Oriented R-CNN        | R-50-FPN | 72.63   | 66.70 | 55.89 | - |2 |  [oriented_rcnn_r50_fpn_1x_dfgovd_le90]()  |[model]()|[log]()| 
| ReDet                 | ReR-50-ReFPN | 72.87   | 67.15 | 56.19 | - |2 |  [redet_re50_refpn_1x_dfgovd_le90]()  |[model]()|[log]()|  
| RoI Transformer       | R-50-FPN | 74.59   | 67.87 | 56.87 | - |2 |  [roi_trans_r50_fpn_1x_dfgovd_le90]()  |[model]()|[log]()|  
| SFRNet                | R-50-FPN | 75.35   | 69.01 | 58.11 | - |2 |  [sfr_oriented_rcnn_r50_fpn_1x_dfgovd_le90]()  |[model]()|[log]()|  
| DRNet                 | R-50-FPN | 77.02   | 68.75 | 58.12 | - |2 |  [drnet_r50_fpn_1x_dfgovd_le90]()  |[model]()|[log]()| 
| PCLDet                | ReR-50-ReFPN | 78.01   | 72.57 | 60.39 | - |2 |  [con_redet_re50_refpn_1x_dfgovd]()  |[model]()|[log]()| 
| PETDet                | ReR-50-ReFPN | 79.56   | 74.47 | 62.23 | - |2 |  [petdet_r50_fpn_1x_dfgovd_le90]()  |[model]()|[log]()| 
