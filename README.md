# G-UNETR++: Liver tumor segmentation
---
![model](./images/model.png)  
  
**🔥G-UNETR++: Liver tumor segmentation from CT images**   
Paper: [G-UNETR++](#)
  
---
# Requirements
Our code is based on [UNETR++](https://github.com/Amshaker/unetr_plus_plus) code.  
But, we modified the code for easy implementation.
Our GPU is `RTX 3090 GPU`.  
  
## Environment
1. Create and activate conda environment  
```bash
conda create --name gunetr_pp python=3.9
conda activate gunetr_pp
```
  
2. Install pytorch
```bash
# cuda 11.3
conda install pytorch==1.12.0 torchvision==0.13.0 torchaudio==0.12.0 cudatoolkit=11.3 -c pytorch
```
It is important that check your `cuda version`.  
Please, see the [pytorch document](https://pytorch.org/get-started/previous-versions/#v1120).  
  
3. Install other dependencies
```
pip install -r requirements.txt
```
  
---
# Dataset
In paper, we teseted `LiTS`, `3Dircadb`, and `Sliver07`.  
  
## Dataset format
```
GUNETR_pplus_LiTS
├── DATASET_Synapse                  
│   ├── unetr_pp_raw
│       ├── unetr_pp_raw_data           
│           ├── Task02_Synapse           
│               ├── Task002_Synapse         
│                   ├── seg_gt
│                       ├── 3Dircadb
│                       ├── LiTS
│                           ├── segmentation-3.nii
│                           ├── ...
│                           └── segmentation-123.nii
│                   ├── unetr_pp_Data_plans_v2.1_stage1
│                       ├── 3Dircadb
│                       ├── LiTS
│                           ├── volume-3.nii
│                           ├── ...
│                           └── volume-123.nii
│                   └── unetr_pp_Plansv2.1_plans_3D.pkl
```
LiTS dataset: [131 cases](https://github.com/Auggen21/LITS-Challenge?tab=readme-ov-file).  
3Dircadb link: [20 cases](https://www.ircad.fr/research/data-sets/liver-segmentation-3d-ircadb-01/).  
> Our LiTS-testset number is `3, 17. 18, 28, 33, 37, 43, 64, 70, 77, 80, 90, 100, 104, 110, and 123`.  
  
## Model Checkpoint
```
GUNETR_pplus_LiTS
├── output_synapse                 
│   ├── 3d_fullres
│       ├── Task002_Synapse                   
│           ├── unetr_pp_trainer_synapse__unetr_pp_Plansv2.1        
│               ├── fold_4
│                   ├── validation_raw
│                   ├── model_final_checkpoint.model
│                   └── model_final_checkpoint.model.pkl
```
Final-model-chekcpoint: [link](https://drive.google.com/drive/folders/1c_Ths-046TQo7p9uSXeOGHxIr3n649KS?usp=sharing).  
  
---
# Implementation
1. Make npy files
```bash
$> python LiTS_npy_make.py
```
You select the options, `LiTS`, and `3Dircadb`.  
  
2. Evaluation script
```bash
$> cd ./evaluation_scripts
$> sh run_evaluation_synapse.sh
```
You select the options, `LiTS`, and `3Dircadb`.  
  
3. Calculation metrics
Please see our [jupyter notebook](https://github.com/AI-Medical-Vision/GUNETR_pplus_Tumor/blob/main/LiTS_metric_Tumor.ipynb).  
We implemented all of metric classes.  
> You can control post-processing option through `flag_post = True`.
  
---
# Result
## LiTS
| Model | DSC | VOE | RAVD | ASSD | RMSD |  
| --- | --- | --- | --- | --- | --- | 
| Chen et al. | 0.711 | 0.401 | 0.023 | 7.201 | 13.445 | 
| Chen et al. | 0.705 | 0.395 | 0.534 | 8.286 | 13.680 | 
| Chen et al. | 0.742 | 0.367 | 0.107 | 5.996 | 10.853 | 
| Jiang et al. | 0.762 | 0.371 | 0.012 | --- | --- | 
| **Ours (G-UNTER++)** | **0.844** | **0.263** | **0.133** | **1.317** | **3.189** | 
  
---
# References
[UNETR++](https://arxiv.org/abs/2212.04497)  
  
---
# Citation
```bibtex
@ARTICLE{
  title={G-UNETR++}, 
  author={},
  journal={}, 
  year={2024},
  doi={}}
```
