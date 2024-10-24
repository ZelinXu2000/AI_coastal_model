> Zelin Xu<sup>1</sup>, Jie Ren<sup>2</sup>, Yupu Zhang<sup>1</sup>, Jose Maria Gonzalez Ondina<sup>3</sup>, Maitane
> Olabarrieta<sup>3</sup>, Tingsong Xiao<sup>1</sup>, Wenchong He<sup>1</sup>, Zibo Liu<sup>1</sup>, Shigang Chen<sup>1</sup>, Kaleb Smith<sup>4</sup>, Zhe Jiang<sup>1</sup> <br>
> *<sup>1</sup>Department of Computer & Information Science & Engineering, University of Florida, Gainesville, FL,
USA<br>
> <sup>2</sup>Department of Computer Science, College of William & Mary, Williamsburg, VA, USA<br>
> <sup>3</sup>Department of Civil & Coastal Engineering, University of Florida, Gainesville, FL, USA<br>
> <sup>4</sup>NVIDIA, Santa Clara, CA, USA*

[[Paper](https://arxiv.org/abs/2410.14952)]

## Abstract

Nearly 900 million people live in low-lying coastal zones around the world and bear the brunt of impacts from more
frequent and severe hurricanes and storm surges. Oceanographers simulate ocean current circulation along the coasts to
develop early warning systems that save lives and prevent loss and damage to property from coastal hazards.
Traditionally, such simulations are conducted using coastal ocean circulation models such as the Regional Ocean Modeling
System (ROMS), which usually runs on an HPC cluster with multiple CPU cores. However, the process is time-consuming and
energy expensive. While coarse-grained ROMS simulations offer faster alternatives, they sacrifice detail and accuracy,
particularly in complex coastal environments. Recent advances in deep learning and GPU architecture have enabled the
development of faster AI (neural network) surrogates. This paper introduces an AI surrogate based on a 4D Swin
Transformer to simulate coastal tidal wave propagation in an estuary for both hindcast and forecast (up to 12 days). Our
approach not only accelerates simulations but also incorporates a physics-based constraint to detect and correct
inaccurate results, ensuring reliability while minimizing manual intervention. We develop a fully GPU-accelerated
workflow, optimizing the model training and inference pipeline on NVIDIA DGX-2 A100 GPUs. Our experiments demonstrate
that our AI surrogate reduces the time cost of 12-day forecasting of traditional ROMS simulations from 9,908 seconds (on
512 CPU cores)  to 22 seconds (on one A100 GPU), achieving over 450$\times$ speedup while maintaining high-quality
simulation results. This work contributes to oceanographic modeling by offering a fast, accurate, and physically
consistent alternative to traditional simulation models, particularly for real-time forecasting in rapid disaster
response.

## Overall Workflow
![workflow](assets/workflow.svg)  
- ROMS historical simulations are pre-processed and used to train the AI surrogate. 
- Trained AI surrogate takes initial and boundary conditions as inputs and predicts the interior values. 
- Verification module: checks physical law adherence of AI predictions and switches to ROMS if the surrogate fails the check.
## Visualization of ROMS and AI surrogate 12-day forecasting results

|              ![u](assets/u.gif)               | 
|:---------------------------------------------:| 
| *Horizontal current velocity $u$ (east-west)* |

|               ![v](assets/v.gif)                | 
|:-----------------------------------------------:| 
| *Horizontal current velocity $v$ (north-south)* |

|     ![zeta](assets/zeta.gif)     | 
|:--------------------------------:| 
| *Free surface elevation $\zeta$* |




